---
tags: [service, cat/storage, scope/in]
aliases: ["RAID 0", "RAID 1"]
---

# RAID Configurations

**RAID (Redundant Array of Independent Disks)** is a technology that combines multiple physical disk drives into a single logical unit to provide data redundancy, performance improvements, or both.

- **RAID 0 (Striping)** - splits data evenly across two or more disks without any redundancy. The main goal is to **increase performance** by allowing read and write operations to happen in parallel across multiple disks.

    It is ideal for applications where performance is critical, but data loss is not a concern, such as video editing or gaming.

- **RAID 1 (Mirroring)** - duplicates the same data on two or more disks. The goal here is to provide **fault tolerance**. If one disk fails, the system can still operate with the remaining disk(s) containing an exact copy of the data.

    It is suitable for systems where data reliability is critical, such as database storage, web servers, or small business file servers.

---
**Up:** [[Amazon EBS]] · **Map:** [[Storage Map]]
