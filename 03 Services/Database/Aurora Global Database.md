---
tags: [service, cat/database, scope/in]
aliases: ["Aurora Global"]
---

# Aurora Global Database

**Aurora Global** - enables a single [[Amazon Aurora|Aurora]] database to span multiple AWS regions, providing low-latency global reads, fast [[Disaster Recovery Strategies|disaster recovery]], and cross-region data replication.

There is 1 primary region for read and write and up to 10 secondary regions for read-only. We can set up to 16 [[RDS Read Replicas|read replicas]] per secondary region. Typical cross-region replication takes less than 1s.

Use **switchover** for planned moves with no data loss, and **failover** for outages. **Write forwarding** lets secondary Regions send writes to the primary.

## Exam tasks
- [[Task 2.2 Design highly available and or or fault-tolerant architectures]]

---
**Up:** [[Amazon Aurora]] · **Map:** [[Database Map]]
