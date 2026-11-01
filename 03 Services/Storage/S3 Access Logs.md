---
tags: [service, cat/storage, scope/in]
---

# S3 Access Logs

**S3 Access Logs** are used for audit purpose, we may want to log all access to [[Amazon S3|S3 buckets]]. Any request made to S3, from any account, authorized or denied will be logged into another S3 bucket. Target logging bucket must be in the same AWS region.

> We should not set our logging bucket to be the monitored bucket. It will create a logging loop and our bucket will grow exponentially.

---
**Up:** [[Amazon S3]] · **Map:** [[Storage Map]]
