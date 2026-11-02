---
tags: [topic, cat/networking, scope/in]
aliases: ["Amazon CloudFront", "CloudFront", "CloudFront Origins", "CloudFront Cache Invalidation", "CloudFront Geo Restriction", "CloudFront Price Classes", "CloudFront Signed URLs and Cookies", "CloudFront Functions and Lambda@Edge", "Lambda@Edge", "OAC", "AWS Global Accelerator", "Global Accelerator", "CloudFront vs Global Accelerator", "Drill CloudFront GlobalAccelerator"]
---

# CloudFront and Global Accelerator

> [!info] Why this matters
> Both services improve global performance, and the exam makes you choose between them. CloudFront is also central to protecting web applications and to reducing load and cost on your origin.
>
> **Covers:** edge services in [[Domain 2 Design Resilient Architectures#Task 2.1|Task 2.1]], [[Domain 3 Design High-Performing Architectures#Task 3.4|Task 3.4]], CDN strategy in [[Domain 4 Design Cost-Optimized Architectures#Task 4.4|Task 4.4]].
> **Study time:** about 3 hours.

## Choosing between them

| | Amazon CloudFront | AWS Global Accelerator |
| --- | --- | --- |
| Purpose | Content delivery network that **caches** content | Routes traffic over the AWS backbone, with **no caching** |
| Protocols | HTTP, HTTPS, WebSocket | TCP and UDP |
| Entry point | A DNS name, and IPs that change | **2 static anycast IPs** |
| Best for | Websites, media, static assets, APIs | Gaming, VoIP, IoT, fast Regional failover |
| Keywords | Cache, CDN, reduce origin load | Static IP, non-HTTP, global failover |

Global **uploads** to one S3 bucket are a third case: [[06 Amazon S3#Performance|S3 Transfer Acceleration]].

## Amazon CloudFront

**CloudFront** serves content from edge locations close to users. When a viewer requests something:

1. The nearest edge location checks its cache.
2. On a hit, it returns the object immediately.
3. On a miss, it fetches from a regional edge cache, or from your origin.
4. It caches the response for next time.

This lowers latency for users, reduces load on your origin, and can lower data transfer cost. Data transfer from AWS origins to CloudFront is free.

CloudFront also provides a security layer: it integrates with **AWS Shield** for DDoS protection and **AWS WAF** for web exploits, and it serves TLS at the edge.

### Origins

| Origin | Notes |
| --- | --- |
| **S3 bucket** | Static content, ideally private behind Origin Access Control |
| **S3 website endpoint** | Custom origin for S3 website features |
| **ALB** | Dynamic content. Can be private with VPC origins |
| **EC2** | Must be reachable, or use VPC origins |
| **API Gateway, Lambda function URL** | Dynamic APIs |
| **Any HTTP server** | Including on-premises |

**VPC origins** let CloudFront reach ALBs, NLBs and EC2 instances in **private subnets**, so that the origin needs no public exposure.

### Keeping S3 origins private

**Origin Access Control (OAC)** lets CloudFront fetch from a private bucket, while the bucket blocks everything else.

1. Create an OAC and attach it to the distribution's S3 origin.
2. Add a bucket policy that allows the CloudFront service principal, for that distribution.
3. Keep Block Public Access on.

**Origin Access Identity (OAI)** is the legacy version. In an exam answer, prefer OAC, and treat OAI as an older distractor.

### Protecting other origins

If an ALB must be public, stop users going around CloudFront by having it add a secret custom header, which the ALB requires. You can also restrict the ALB's security group to CloudFront's managed prefix list.

### Caching

A **cache behaviour** matches a path pattern, such as `/images/*`, and sets the origin, allowed methods, TTLs and what forms the cache key.

- **TTLs** come from `Cache-Control` and `Expires` headers, within limits you set. The default is 24 hours.
- The **cache key** is what makes two requests "the same". Fewer headers, cookies and query strings in the key means a **higher cache hit ratio**.
- **Origin Shield** adds an extra caching layer in front of the origin, to reduce origin load further.

If the origin changes, CloudFront keeps serving the cached copy until the TTL expires. To force a refresh, either:

- Run an **invalidation** on specific paths or `/*`. This has a cost beyond a free allowance.
- Use **versioned file names**, such as `style.v2.css`. This is often the better long-term design.

### HTTPS

- **Viewer protocol policy** controls HTTP and HTTPS between the user and the edge. It can redirect HTTP to HTTPS.
- **Origin protocol policy** controls the connection between the edge and the origin.
- A custom domain needs an [[23 Encryption and Secrets#AWS Certificate Manager|ACM]] certificate in **us-east-1**, whatever the Region of your application.
- SNI lets many domains share edge IPs.

### Restricting content

| Feature | Use |
| --- | --- |
| **Signed URLs** | Access to individual files, or clients that do not support cookies |
| **Signed cookies** | Access to many files, such as a whole subscriber library, or when you do not want to change URLs |
| **Geo restriction** | Allow or block countries, using a third-party Geo-IP database |
| **WAF** | Rules such as rate limits |

### Signed URLs and signed cookies

Your application decides who is allowed, then gives them a signed URL or cookie with an expiry time. CloudFront validates the signature at the edge. The memory aid: **one file, signed URL; many files, signed cookies.**

| | CloudFront signed URL | S3 presigned URL |
| --- | --- | --- |
| Served through | CloudFront | S3 directly |
| Origin | Any | S3 only |
| Signed with | A CloudFront key pair | The identity of an IAM principal |
| Filters | IP range, path, dates | Expiry only |

### Availability

**Origin failover** uses an origin group, with a primary and a secondary origin. If the primary returns an error code such as 500 or 503, or does not respond, CloudFront retries against the secondary. It works for GET, HEAD and OPTIONS requests only. A typical use is two S3 buckets with Cross-Region Replication.

### Price classes and pricing plans

**Price classes** limit which edge locations are used, in exchange for lower cost.

| Class | Edge locations | Trade-off |
| --- | --- | --- |
| Price Class All | All | Best performance, highest cost |
| Price Class 200 | Most Regions, excluding the most expensive | Middle ground |
| Price Class 100 | North America and Europe | Lowest cost |

AWS also now offers **flat-rate plans** that bundle CDN, WAF, DNS and DDoS protection for a fixed monthly price, with no overage charges. They are a newer option, so older questions assume pay-as-you-go.

### Edge functions

| | CloudFront Functions | Lambda@Edge |
| --- | --- | --- |
| Runtime | JavaScript | Node.js, Python |
| Triggers | Viewer request and response | Viewer and origin, request and response |
| Run time | Under 1 millisecond | Seconds |
| Memory | 2 MB | Up to 10 GB |
| Scale | Millions of requests per second | Thousands per second |
| Network and body access | No | Yes |
| Use | Header changes, redirects, URL rewrites, simple auth | Heavier logic, external calls, image transformation |

Choose the lighter option unless you need network access, a request body, or origin-side triggers. Lambda@Edge functions are authored in us-east-1 and replicated to edge locations.

**Field-level encryption** can encrypt specific sensitive form fields at the edge, so that only the application holding the private key can read them.

### Logging and monitoring

- **Standard logs** record each request, and are delivered to S3 or other destinations.
- **Real-time logs** go to Kinesis Data Streams within seconds.
- **CloudWatch metrics** show requests, error rates and cache statistics.

### Example of cache behaviours

One distribution can serve a whole site, with different rules for each path.

| Path pattern | Origin | Caching |
| --- | --- | --- |
| `/images/*` | S3 | Long TTL |
| `/api/*` | ALB | Caching off, with headers and cookies forwarded |
| Default (`*`) | S3 | Medium TTL |

## AWS Global Accelerator

**Global Accelerator** gives you **two static anycast IPv4 addresses**. Dual-stack accelerators add two IPv6 addresses. Users connect to the nearest edge location, and traffic then travels over the AWS global network to your application.

- **Endpoints:** ALB, NLB, EC2 instances and Elastic IPs.
- **Endpoint groups:** one per Region. **Traffic dials** control how much goes to each Region.
- **Endpoint weights:** split traffic inside a Region, for blue/green deployment.
- **Health checks:** unhealthy endpoints are avoided, and failover usually takes less than a minute, without any DNS change.
- **Client IP preservation** is available for supported endpoints.
- **Shield Standard** protects it.
- **Custom routing accelerators** map users to specific EC2 destinations, as used by some multiplayer games.

The static IPs stay yours until you delete the accelerator, so customers can allow-list them. This solves the "ALB has no static IP" problem globally.

## Exam patterns

| If the question says | Think | Why |
| --- | --- | --- |
| Static website worldwide, bucket must not be public | CloudFront with S3 and OAC | |
| Subscribers stream any video in a library | Signed cookies | Many files |
| Send a customer a link to one report | Signed URL | One file |
| Licensing forbids some countries | Geo restriction | Country level at the edge |
| Reduce origin load | Longer TTL, higher cache hit ratio, Origin Shield | |
| Users see old content after an update | Invalidation or versioned names | |
| Custom domain certificate on CloudFront | ACM in us-east-1 | Always |
| Private ALB behind CloudFront | VPC origins | |
| Serve from a second origin if the first fails | Origin group | GET, HEAD, OPTIONS |
| Reduce CloudFront bill, users in US and Europe | Price Class 100 | |
| Add a security header at the edge | CloudFront Functions | Lightweight |
| Resize images on request | Lambda@Edge | Needs more compute |
| Protect a site from SQL injection at the edge | WAF on CloudFront | |
| UDP game traffic | Global Accelerator | CloudFront is HTTP |
| Fixed IPs for customer firewalls | Global Accelerator | Two anycast IPs |
| Regional failover without DNS caching delay | Global Accelerator | |
| Global uploads to one bucket | Transfer Acceleration | Not CloudFront |

## Check yourself

**1.** A company hosts a static site in S3 and serves it worldwide. The bucket must not be publicly accessible. What should the architect do?

- A. Enable S3 static website hosting and a public bucket policy
- B. Use CloudFront with Origin Access Control and a bucket policy for CloudFront
- C. Use an ALB in front of S3
- D. Use Global Accelerator with S3

> [!success]- Answer
> **B.** OAC keeps the bucket private, and CloudFront serves the content.

**2.** A streaming service must give paying subscribers access to thousands of video segments without changing its URLs. What should it use?

- A. Signed URLs
- B. Signed cookies
- C. S3 presigned URLs
- D. Geo restriction

> [!success]- Answer
> **B.** Signed cookies cover many files and leave the URLs unchanged.

**3.** A multiplayer game uses UDP, and global players report high latency. Which service helps most?

- A. CloudFront
- B. Global Accelerator
- C. S3 Transfer Acceleration
- D. API Gateway

> [!success]- Answer
> **B.** It supports UDP and carries traffic on the AWS backbone. CloudFront handles HTTP.

**4.** Customers' firewalls allow only fixed IP addresses. The application runs behind ALBs in two Regions. What should the architect do?

- A. Assign Elastic IPs to the ALBs
- B. Put Global Accelerator in front of the ALBs
- C. Use CloudFront signed cookies
- D. Use Route 53 Multivalue routing

> [!success]- Answer
> **B.** Its two static anycast IPs can be allow-listed and can route to both Regions.

**5.** After updating files in S3, users still see old versions through CloudFront for many hours. What is the quickest way to fix this?

- A. Delete the S3 bucket
- B. Create a CloudFront invalidation
- C. Change the price class
- D. Enable Origin Shield

> [!success]- Answer
> **B.** An invalidation removes objects from the caches, so the next request fetches the new version.

**6.** An engineer wants to attach an ACM certificate to a CloudFront distribution. The application runs in eu-west-1. Where must the certificate be?

- A. eu-west-1
- B. us-east-1
- C. Any Region
- D. The same AZ as the origin

> [!success]- Answer
> **B.** CloudFront only uses ACM certificates in us-east-1.

**7.** A company wants to add a security header to every response and rewrite some URLs at very high scale, at the lowest cost. Which feature should it use?

- A. Lambda@Edge
- B. CloudFront Functions
- C. EC2 at the origin
- D. Step Functions

> [!success]- Answer
> **B.** This is lightweight header and URL work, which CloudFront Functions are designed for.

**8.** A website's origin is overloaded even though it sits behind CloudFront. The cache hit ratio is low, because all query strings and cookies are forwarded to the origin. What should the team do? (Choose two.)

- A. Reduce the cache key to only what the content depends on
- B. Increase TTLs where appropriate
- C. Turn off CloudFront
- D. Use a NAT gateway
- E. Decrease TTLs to zero

> [!success]- Answer
> **A and B.** A narrower cache key and longer TTLs mean more requests are answered at the edge.

**9.** A company must run the same origin in two Regions, serving from the secondary if the primary returns 503 errors. Both buckets hold the same content. Which CloudFront feature fits?

- A. Geo restriction
- B. Origin group failover
- C. Price classes
- D. Field-level encryption

> [!success]- Answer
> **B.** An origin group retries the secondary origin for configured error codes.

---
**Previous:** [[11 Route 53]] · **Next:** [[13 RDS and Aurora]] · **Plan:** [[Study Guide]]
