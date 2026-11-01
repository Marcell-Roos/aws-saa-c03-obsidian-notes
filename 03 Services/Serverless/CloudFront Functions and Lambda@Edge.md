---
tags: [service, cat/serverless, scope/in]
aliases: ["Lambda@Edge", "CloudFront Functions", "Edge Function"]
---

# CloudFront Functions and Lambda@Edge

**Edge Function** - a code that we write and attach to [[Amazon CloudFront|CloudFront]] distributions. It runs close to our users to minimize latency. CloudFront provides two types: **CloudFront Functions** & **Lambda@Edge**. We don't have to manage any servers (fully serverless, pay only for what we use) and it is deployed globally.

Use cases: website security, dynamic web app at the edge, SEO (Search Engine Optimization), bot mitigation at the edge, real-time image transformation …

**CloudFront Functions** - lightweight functions written in JavaScript. Used for high-scale, latency-sensitive CDN customizations (sub-ms startup times, millions of requests/second).

They are used to change viewer requests and responses.

- Viewer Request - after CloudFront receives a request from a viewer.
- Viewer Response - before CloudFront forwards the response to the viewer.

**Lambda@Edge** - [[AWS Lambda|Lambda functions]] written in NodeJS or Python. It scales to 1000s of requests/seconds. They are used to change CloudFront requests and responses.

- Origin Request - before CloudFront forwards the request to the origin.
- Origin Response - after CloudFront receives the response from the origin.

Author our functions in one AWS Region (us-east-1), then CloudFront replicates to its locations.

**CloudFront Functions vs Lambda@Edge**

The source had this comparison only as an image.

| | CloudFront Functions | Lambda@Edge |
| --- | --- | --- |
| Runtime | JavaScript | Node.js, Python |
| Trigger | Viewer request and response | Viewer and origin, request and response |
| Max run time | Sub-millisecond | Seconds |
| Network and body access | No | Yes |
| Use | Header changes, redirects, URL rewrite | Heavier logic, external calls |

---
**Up:** [[Amazon CloudFront]] · **Map:** [[Serverless Map]]
