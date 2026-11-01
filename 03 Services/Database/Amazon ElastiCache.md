---
tags: [service, cat/database, scope/in]
aliases: ["ElastiCache"]
---

# Amazon ElastiCache

**Amazon ElastiCache** is a fully managed, in-memory caching service provided by AWS. ElastiCache supports three in-memory engines: **Valkey** (the open-source Redis fork), plus the two below. It can run as a serverless cache or as a node-based cluster.

- **Redis** - in-memory data structure store that supports data types like strings, hashes, lists…
- **Memcached** - a high-performance, distributed memory object caching system. It is simple and ideal for use cases that require a large cache with minimal operational overhead.

ElastiCache helps reduce load off databases for read intensive workloads. Using ElastiCache involves heavy application code changes.

**ElastiCache** **Auto Discovery** - the ability for client programs to automatically identify all of the nodes in a cache cluster, and to initiate and maintain connections to all of these nodes.

**[[Redis vs Memcached]]**

- **Solution Architecture - DB Cache.**

    It is used to reduce the latency and load on a relational or NoSQL database by caching frequently accessed data.

    **Components:**

    - **Amazon ElastiCache (Redis/Memcached)**
    - **Primary Database ([[Amazon RDS|RDS]]/DynamoDB)**
    - **Application**

    Cache must have an invalidation strategy to make sure only the most current data is used in there.

- **Solution Architecture - User Session Store.**

    Used to manage user session data efficiently by storing it in an in-memory cache, providing fast access and improving application performance.

    **Components:**

    - **Amazon ElastiCache (Redis)**
    - **Application Servers**
    - **User Database (Optional)**

    User logs into any of the application instances. The application writes the session data into ElastiCache. Then the user hits another instance of our application and instance retrieves the data and the user is already logged in.

- Managed Redis/Memcached (similar offering as RDS, but for caches).
- In-memory data store, sub-millisecond latency.
- Select an ElastiCache instance type (e.g, cache.m6g.large).
- Support for Clustering (Redis) and Multi AZ, [[RDS Read Replicas|Read Replicas]] (sharding).
- Security through [[AWS IAM|IAM]], [[Security Groups]], [[AWS KMS|KMS]], Redis Auth.
- Backup/Snapshot/PITR feature.
- Managed and scheduled maintenance.
- **Requires some application code changes to be leveraged**.
- Used for key/value store, frequent reads, less writes, cache results for DB queries, store session data for websites, cannot use SQL.

Valkey and Redis OSS share features, and ElastiCache Serverless needs no capacity planning. See [[Redis vs Memcached]].

## In this topic
- [[Caching Strategies]]
- [[ElastiCache Cluster Modes]]
- [[ElastiCache High Availability]]
- [[ElastiCache Security]]

## Exam tasks
- [[Task 3.3 Determine high-performing database solutions]]

---
**Map:** [[Database Map]]
