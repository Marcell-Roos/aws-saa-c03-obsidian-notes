---
tags: [service, cat/storage, scope/in]
---

# S3 Versioning

Version for files can be enabled in [[Amazon S3]]. It is enabled at the bucket level. Same key overwrite will change the versions.

It’s best practice to version our buckets. It protects us against unintended deletes (can restore a version) and we can roll back to previous version easily.

Any file that is not versioned prior to enabling versioning will have “null” version. Suspending versioning does not delete the previous versions.

## Exam tasks
- [[Task 1.3 Determine appropriate data security controls]]

---
**Up:** [[Amazon S3]] · **Map:** [[Storage Map]]
