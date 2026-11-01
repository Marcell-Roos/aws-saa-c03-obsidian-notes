---
tags: [service, cat/storage, scope/in]
aliases: ["S3 Transfer Acceleration", "Transfer Acceleration", "multipart upload", "Multi-Part Upload", "Byte-Range Fetches"]
---

# S3 Performance

[[Amazon S3|S3]] automatically scales to high request rates, latency 100-200ms. Our application can achieve at least 3500 PUT/COPY/POST/DELETE or 5500 GET/HEAD requests per second per prefix in a bucket. If we spread reads across all four prefixes evenly, we can achieve 22000 requests per second for GET and HEAD.

**Performance Boosts**

- **Multi-Part Upload** - recommended for files over 100 MB, required for objects over 5 GiB. It can help parallelize uploads.

- **S3 Transfer Acceleration** - increase transfer speed by transferring file to an AWS [[AWS Global Infrastructure|Edge Location]] which will forward the data to the S3 bucket in the target region. It is compatible with multi-part upload.

- **S3 Byte-Range Fetches** - parallelizes GETs by requesting specific byte ranges. It has better resilience in case of failures. Can be used to speed up downloads and to retrieve only partial data.

## Exam tasks
- [[Task 3.1 Determine high-performing and or or scalable storage solutions]]

---
**Up:** [[Amazon S3]] · **Map:** [[Storage Map]]
