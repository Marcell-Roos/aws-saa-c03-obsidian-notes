---
tags: [service, cat/storage, scope/in]
aliases: ["Multi-Attach"]
---

# EBS Multi-Attach

**Multi-Attach** lets us to attach same [[Amazon EBS|EBS volume]] to multiple [[Amazon EC2|EC2 instances]] in the same AZ. It is only possible with io1/io2 volume types. Each EC2 instance has full read and write permissions to the high-performance volume.

It’s **limited to 16 EC2 instances at a time** and we must use a file system that’s cluster-aware (not XFS, EXT4, etc).

Use cases:

- Achieving higher application availability in clustered Linux applications.
- If applications must manage concurrent write operations.

It needs Nitro-based instances. Windows supports Multi-Attach with io2 only.

---
**Up:** [[Amazon EBS]] · **Map:** [[Storage Map]]
