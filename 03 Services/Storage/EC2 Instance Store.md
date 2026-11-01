---
tags: [service, cat/storage, scope/in]
aliases: ["Instance Store", "instance store"]
---

# EC2 Instance Store

[[Amazon EBS|EBS volumes]] have “limited” performance. If we need high performance hardware disk, we should use **EC2 Instance Store**.

EC2 Instance Store has better I/O performance and they are good for buffer, **cache**, scratch data or temporary content.

EC2 Instance Store lose their storage if they are stopped (ephemeral). So we have risk of data loss if hardware fails. Backups and replication are our responsibility.

## Exam tasks
- [[Task 3.1 Determine high-performing and or or scalable storage solutions]]

---
**Up:** [[Amazon EBS]] · **Map:** [[Storage Map]]
