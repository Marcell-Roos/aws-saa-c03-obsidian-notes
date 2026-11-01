---
tags: [service, cat/storage, scope/in]
aliases: ["Access Points"]
---

# S3 Access Points

**Access Points** simplify security management for [[Amazon S3|S3]] Buckets. Each Access Point has its own [[DNS Fundamentals|DNS]] name (Internet Origin or [[Amazon VPC|VPC]] Origin) and access point policy (similar to [[S3 Access Control|bucket policy]]).

We **can define the access point to be accessible only from within the VPC**. To do that we must create a [[VPC Endpoints|VPC Endpoint]] to access the Access Point and the VPC Endpoint must allow access to the target bucket and Access Point.

---
**Up:** [[Amazon S3]] · **Map:** [[Storage Map]]
