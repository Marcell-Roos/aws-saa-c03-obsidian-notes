---
tags: [service, cat/storage, scope/in]
aliases: ["S3", "S3 bucket", "S3 buckets"]
---

# Amazon S3

**Amazon S3** is one of the main building blocks of AWS (advertised as “infinitely scaling” storage).

S3 use cases: backup and storage, [[Disaster Recovery Strategies|disaster recovery]], archive, hybrid cloud storage, application hosting, media hosting, [[Data Lakes|data lakes]], software delivery, static website …

Amazon S3 allows people to store objects (files) in “**buckets**” (directories). Buckets must have a globally unique name (across all regions all accounts). Buckets are defined at the region level (S3 looks like a global service but buckets are created in a region).

Objects have a key. The key is FULL path (for example s3://my-bucket/folder1/folder2/file.txt). The key is composed of prefix+object name. There is no concept of “directories” within buckets, just keys with very long names that contain slashes.

**Object values** are content of the body. Max object size is 48.8 TiB (raised from the long-standing 5 TB limit), and anything over 5 GiB must use [[S3 Performance|multipart upload]]. Object can have also **metadata** (list of text key/value pairs), **tags** (unicode key/value pair, useful for security/lifecycle), **version ID**.

**Consistency:** S3 gives strong read-after-write consistency. **Durability:** 11 nines. **New options:** directory buckets (S3 Express One Zone) and S3 Tables for Apache Iceberg data.

## In this topic
- [[Amazon S3 Glacier]]
- [[S3 Access Control]]
- [[S3 Access Logs]]
- [[S3 Access Points]]
- [[S3 Batch Operations]]
- [[S3 CORS]]
- [[S3 Encryption]]
- [[S3 Event Notifications]]
- [[S3 Lifecycle Rules]]
- [[S3 MFA Delete]]
- [[S3 Multi-Region Access Points]]
- [[S3 Object Lambda]]
- [[S3 Object Lock and Glacier Vault Lock]]
- [[S3 Performance]]
- [[S3 Pre-Signed URLs]]
- [[S3 Replication]]
- [[S3 Requester Pays]]
- [[S3 Select]]
- [[S3 Storage Classes]]
- [[S3 Storage Lens]]
- [[S3 Versioning]]

## Exam tasks
- [[Task 3.1 Determine high-performing and or or scalable storage solutions]]

---
**Map:** [[Storage Map]]
