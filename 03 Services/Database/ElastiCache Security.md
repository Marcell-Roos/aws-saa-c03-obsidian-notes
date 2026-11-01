---
tags: [service, cat/database, scope/in]
aliases: ["Redis AUTH"]
---

# ElastiCache Security

**Cache Security**

[[Amazon ElastiCache|ElastiCache]] supports [[AWS IAM|IAM]] authentication for Redis. [[IAM Policy Structure|IAM policies]] on ElastiCache are only used for API-level security.

**Redis AUTH** - we can set a password/token when we create a Redis cluster. This is an extra level of security for our cache (on top of [[Security Groups|security groups]]). It supports SSL in-flight encryption.

To require that users enter a password on a password-protected Redis server, include the parameter --auth-token with the correct password when we create our replication group or cluster and on all subsequent commands to the replication group or cluster.

Memcached supports SASL-based authentication.

---
**Up:** [[Amazon ElastiCache]] · **Map:** [[Database Map]]
