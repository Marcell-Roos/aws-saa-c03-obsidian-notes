---
tags: [service, cat/database, scope/in]
---

# ElastiCache High Availability

**Replication Groups** are collections of Redis nodes (instances) where one is the **primary** node that handles writes, and the rest are **replica nodes** that handle reads and provide failover if the primary fails.

Shard in Redis is a subset of the dataset. In sharding, data is split across multiple Redis nodes, which helps with **[[Scalability and High Availability|horizontal scaling]]**. A shard can have a primary node and multiple replica nodes to provide redundancy and availability.

Redis supports a persistence mode called **Append-Only File (AOF)**. Every write operation is logged in an append-only file, ensuring that no data is lost in case of failure. AOF provides **data durability** but may slightly degrade performance because of disk writes. AOF only protects against node restarts, not hardware or AZ failure, and in [[Amazon ElastiCache|ElastiCache]] for Redis OSS it is mutually exclusive with Multi-AZ. For resilience we should use Multi-AZ replication groups with automatic failover instead.

---
**Up:** [[Amazon ElastiCache]] · **Map:** [[Database Map]]
