---
tags: [comparison, scope/in]
---

# RDS Multi-AZ vs Read Replicas vs Aurora Global

| | [[RDS Multi-AZ]] instance | Multi-AZ DB cluster | [[RDS Read Replicas]] | [[Aurora Global Database]] |
| --- | --- | --- | --- | --- |
| Purpose | Availability | Availability + reads | Read scaling | Global reads and DR |
| Replication | Synchronous | Semi-synchronous | Asynchronous | Asynchronous, storage-based |
| Readable standby | No | Yes, 2 | Yes, up to 15 | Yes |
| Scope | Region | Region, 3 AZs | AZ, cross-AZ or cross-Region | Up to 10 secondary Regions |
| Failover | Automatic | Automatic | Manual promotion | Managed |

---
**Up:** [[Comparisons Map]]
