---
tags: [service, cat/storage, scope/in]
---

# S3 Batch Operations

With **S3 Batch Operations** we can perform bulk operations on existing [[Amazon S3|S3]] objects with a single request. A job consists of a list of objects, the action to perform and optional parameters. S3 Batch Operations manages retries, tracks progress, sends completion notifications and generate reports.

Use cases:

- Modify object metadata & properties.
- Copy objects between S3 buckets.
- **Encrypt un-encrypted objects.**
- Modify ACLs
- Restore objects from [[Amazon S3 Glacier|S3 Glacier]]
- Invoke [[AWS Lambda|Lambda function]] to perform custom action on each object.

We can use S3 Inventory to get object list and use [[S3 Select]] to filter our objects.

---
**Up:** [[Amazon S3]] · **Map:** [[Storage Map]]
