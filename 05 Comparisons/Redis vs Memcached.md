---
tags: [comparison, scope/in]
---

# Redis vs Memcached

The source had this only as an image.

| | Valkey or Redis OSS | Memcached |
| --- | --- | --- |
| Data types | Complex: lists, sets, sorted sets | Simple |
| Replication and failover | Yes, Multi-AZ | No |
| Backups | Yes | No |
| Threads | Mostly single | Multi-threaded |
| Use | Leaderboards, sessions, durability needs | Simple cache, scale out |

See [[Amazon ElastiCache]].

---
**Up:** [[Comparisons Map]]
