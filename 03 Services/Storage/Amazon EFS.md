---
tags: [service, cat/storage, scope/in]
aliases: ["EFS"]
---

# Amazon EFS

**EFS** is managed NFS (network file system) that can be mounted on hundreds of [[Amazon EC2|EC2]]. EFS works with **Linux** (uses POSIX file system) EC2 instances in multi-AZ. It uses NFSv4.1 protocol.

We can enable [[Encryption at Rest and in Transit|encryption at rest]] using [[AWS KMS|KMS]].

EFS is highly available, scalable, expensive, pay per use and has no capacity planning.

EFS can handle 1000s of concurrent NFS clients. Grows to petabyte-scale network file system automatically.

- **Solution Architecture - Mounting EFS with on-premises Linux Clients.**

    We can mount our EFS file systems on our on-premises data center servers when connected to our [[Amazon VPC|VPC]] with [[AWS Direct Connect|DX]] or VPN.

**EFS Replication** copies a file system to another Region or AZ for DR. **One Zone** storage costs less for data that doesn't need multi-AZ.

## In this topic
- [[EFS Performance and Throughput]]
- [[EFS Storage Classes]]

## Exam tasks
- [[Task 3.1 Determine high-performing and or or scalable storage solutions]]
- [[Task 4.1 Design cost-optimized storage solutions]]

---
**Map:** [[Storage Map]]
