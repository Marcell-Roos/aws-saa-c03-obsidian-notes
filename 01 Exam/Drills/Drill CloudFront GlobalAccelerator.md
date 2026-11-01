---
tags: [drill, scope/in]
---

# Drill CloudFront GlobalAccelerator

Adapted from [RonitSachdev/aws-saa-c03-guides](https://github.com/RonitSachdev/aws-saa-c03-guides) (CC BY 4.0), with outdated facts changed.

## Question patterns

- *"Serve a static website to users worldwide with low latency; the [[Amazon S3|S3 bucket]] must not be publicly accessible"* → **[[Amazon CloudFront|CloudFront]] + S3 origin + [[CloudFront Origins|OAC]]** (cache at edges, lock the bucket to CloudFront only).
- *"Paying subscribers should stream any video in the premium catalog"* → **Signed Cookies** (MANY files = cookies; ONE file = signed URL).
- *"Send a customer a link to download a single report"* → **Signed URL** (one file, one URL).
- *"Multiplayer game over UDP has high latency for global players"* → **[[AWS Global Accelerator|Global Accelerator]]** (UDP rules out CloudFront instantly).
- *"Enterprise clients' firewalls require a small set of FIXED IP addresses to whitelist"* → **Global Accelerator** (2 static anycast IPs — the only global service that offers this).
- *"Multi-region app needs failover in seconds, without waiting for [[DNS Fundamentals|DNS]] caches"* → **Global Accelerator** (in-path health checks, same IPs before and after).
- *"Licensing forbids streaming the content in certain countries"* → **[[CloudFront Geo Restriction]]** (country-level block at the edge).
- *"Reduce the load on the origin server behind CloudFront"* → **Increase TTL / improve cache hit ratio** (more hits at the edge = fewer origin fetches).
- *"Users around the world upload large files into one S3 bucket, uploads are slow"* → **[[S3 Performance|S3 Transfer Acceleration]]** (UPLOAD direction — not CloudFront).
- *"Attach a custom domain certificate to a CloudFront distribution"* → **[[AWS Certificate Manager|ACM]] certificate in us-east-1** (always, regardless of your app's region).

## Pocket card

| Keyword in question | Answer |
|---|---|
| global static content, low latency | **CloudFront** |
| "S3 only via CloudFront", private bucket | **OAC** (OAI = legacy distractor) |
| one paid file | **Signed URL** |
| whole paid library | **Signed Cookies** |
| block/allow countries | **Geo Restriction** |
| CloudFront custom cert | **ACM in us-east-1** |
| encrypt one sensitive field end-to-end | Field-level encryption |
| reduce origin load | Longer TTL / better caching |
| force-refresh cached files | Invalidation (`/*`, costs money) |
| UDP / gaming / VoIP / non-HTTP | **Global Accelerator** |
| fixed IPs for whitelisting | **Global Accelerator** (2 anycast IPs) |
| instant failover, no DNS-cache lag | **Global Accelerator** |
| global UPLOADS to S3 | **S3 Transfer Acceleration** |

---
**Up:** [[Drills Map]]
