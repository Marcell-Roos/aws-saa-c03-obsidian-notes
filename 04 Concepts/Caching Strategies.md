---
tags: [concept, scope/in]
aliases: ["Lazy Loading", "Write Through", "caching strategies"]
---

# Caching Strategies

**[[Amazon ElastiCache|ElastiCache]] Design Patterns**

- **Lazy Loading (Cache-Aside)** - all the read data is cached, data can become stale in cache.

- **Write Through** - adds or updates data in the cache written to a database (no stale data).

- **Session Store** - store temporary session data in a cache (using TTL features).

**ElastiCache - Redis Use Case**

Gaming leaderboards are computationally complex and Redis sorted sets guarantee both uniqueness and element ordering to solve this problem. Each time a new element is added, it is ranked in real time, then added in correct order.

## Exam tasks
- [[Task 2.1 Design scalable and loosely coupled architectures]]
- [[Task 3.3 Determine high-performing database solutions]]
- [[Task 4.3 Design cost-optimized database solutions]]

---
**Up:** [[Amazon ElastiCache]]
