---
tags: [service, cat/storage, scope/in]
aliases: ["Lustre"]
---

# FSx for Lustre

**FSx for Lustre** - type of **parallel** distributed file system, for large-scale computing. It is commonly used for HPC and uses ML. We can chose between SSD and HDD storage options. Can be used from on-premises servers (VPN or [[AWS Direct Connect|Direct Connect]]).

FSx for Lustre uses a striped architecture, where data is distributed across multiple disks to optimize performance.

We can read [[Amazon S3|S3]] as a file system through [[Amazon FSx|FSx]] and write the output of the computations back to S3 (through FSx).

- **Solution Architecture - Automate File Retrieval from [[Amazon S3 Glacier|S3 Glacier]].** Restore archived objects to S3, then link the bucket to FSx for Lustre for high-speed access during processing.

## Exam tasks
- [[Task 3.1 Determine high-performing and or or scalable storage solutions]]

---
**Up:** [[Amazon FSx]] · **Map:** [[Storage Map]]
