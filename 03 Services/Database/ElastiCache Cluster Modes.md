---
tags: [service, cat/database, scope/in]
aliases: ["Cluster Mode", "cluster mode"]
---

# ElastiCache Cluster Modes

| | Cluster mode disabled | Cluster mode enabled |
| --- | --- | --- |
| Shards | 1 | Up to many, data partitioned |
| Replicas | Up to 5 per shard | Up to 5 per shard |
| Scales | Reads | Reads and writes |

Use it enabled when data won't fit one node or when writes must scale.

---
**Up:** [[Amazon ElastiCache]] · **Map:** [[Database Map]]
