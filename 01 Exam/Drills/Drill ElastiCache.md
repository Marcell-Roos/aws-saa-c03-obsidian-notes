---
tags: [drill, scope/in]
---

# Drill ElastiCache

Adapted from [RonitSachdev/aws-saa-c03-guides](https://github.com/RonitSachdev/aws-saa-c03-guides) (CC BY 4.0), with outdated facts changed.

## Question patterns

- *"Popular product pages generate thousands of identical reads that overload [[Amazon RDS|RDS]]"* → **[[Amazon ElastiCache|ElastiCache]]** (repeated reads belong in memory)
- *"Real-time gaming leaderboard with player rankings"* → **Redis sorted sets** (ranking is built in — free points)
- *"Users get logged out when the Auto Scaling Group terminates instances"* → **store sessions in ElastiCache for Redis** (make the web tier [[Stateless and Stateful Workloads|stateless]])
- *"Cache must survive a node failure without data loss"* → **Redis** (replication + Multi-AZ failover; Memcached has neither)
- *"Simplest cache, multithreaded, losing cached data is fine"* → **Memcached** (the only time it wins)
- *"Cached prices must never be out of date"* → **write-through** (cache updated on every write; lazy loading can serve stale)
- *"Long analytical/reporting queries slow the production database"* → **[[RDS Read Replicas|Read Replica]]**, not a cache (diverse queries never hit cache)
- *"Speed up [[Amazon DynamoDB|DynamoDB]] reads without modifying the application"* → **[[DynamoDB Accelerator|DAX]]** (ElastiCache would require code changes)
- *"Publish/subscribe messaging between app components using the cache layer"* → **Redis** (pub/sub is Redis-only)

## Pocket card

| Keyword | Answer |
|---|---|
| Repeated identical reads hammering DB | ElastiCache |
| Leaderboard / ranking | Redis sorted sets |
| Sessions / stateless web tier | Redis (or DynamoDB) |
| Durability, failover, backup, pub/sub | Redis |
| Simplest, multithreaded, loss OK | Memcached |
| Never-stale cache | Write-through |
| Stale-tolerant, cache only hot data | Lazy loading (+ TTL) |
| Diverse/analytical read offload | Read Replica |
| DynamoDB + no code change | DAX |
| Microseconds | Any in-memory cache (ElastiCache/DAX) |

---
**Up:** [[Drills Map]]
