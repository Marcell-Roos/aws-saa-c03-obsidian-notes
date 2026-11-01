---
tags: [concept, scope/in]
aliases: ["stateless", "stateful"]
---

# Stateless and Stateful Workloads

A **stateless** tier keeps no session data on the instance, so any instance can serve any request and [[Scalability and High Availability|horizontal scaling]] is simple. A **stateful** tier keeps data locally, which makes scaling and failover harder.

Move state out of the instance:

- Sessions to [[Amazon ElastiCache]] or [[Amazon DynamoDB]]
- Files to [[Amazon S3]] or [[Amazon EFS]]
- Relational data to [[Amazon RDS]] or [[Amazon Aurora]]

[[ELB Sticky Sessions]] are a workaround, not a fix.

## Exam tasks
- [[Task 2.1 Design scalable and loosely coupled architectures]]

---
**Up:** [[Concepts Map]]
