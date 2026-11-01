---
tags: [service, cat/migration, scope/in]
aliases: ["DataSync"]
---

# AWS DataSync

**DataSync** is used to automate and accelerate the replication of data and move large amount of data to and from on-premises to AWS (need agent) or AWS to AWS. It can synchronize to **[[Amazon S3|S3]], [[Amazon EFS|EFS]]** and **[[Amazon FSx|FSx]]**. Replication tasks can be scheduled hourly, daily or weekly.

File permissions and metadata are preserved (NFS POSIX, SMB…). One agent task can use 10 Gbps and we can setup a bandwidth limit.

The DataSync agent can route DataSync traffic from the on-premises storage system (source location) to the [[AWS Direct Connect|DX]] connection.

## Exam tasks
- [[Task 3.5 Determine high-performing data ingestion and transformation solutions]]
- [[Task 4.1 Design cost-optimized storage solutions]]

---
**Map:** [[Migration and Transfer Map]]
