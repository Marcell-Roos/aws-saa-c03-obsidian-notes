---
tags: [service, cat/networking, scope/in]
aliases: ["OAC", "Origin Access Control", "OAI"]
---

# CloudFront Origins

**CloudFront Origins**

- [[Amazon S3|S3 bucket]]

    Used for distributing files and caching them at the [[AWS Global Infrastructure|edge location]]. Enhanced security with [[Amazon CloudFront|CloudFront]] **Origin Access Control (OAC)**. It can be used as an ingress (to upload files to S3).

- Custom Origin (HTTP)

    It can be **[[Application Load Balancer|ALB]], [[Amazon EC2|EC2 instance]] or S3** **website** (must enable the bucket as a static S3 website).

**Origin Access Identity (OAI)** is the legacy way to give CloudFront access to an S3 bucket. AWS recommends OAC instead.

---
**Up:** [[Amazon CloudFront]] · **Map:** [[Networking and Content Delivery Map]]
