---
tags: [service, cat/database, scope/in]
aliases: ["Read Replicas", "read replicas", "Read Replica", "read replica"]
---

# RDS Read Replicas

**Read Replicas**

**Read Replicas** are a feature that allows us to create one or more read-only copies (max 15; AWS recommends no more than 5 for Oracle) of our primary database instance. They can be within AZ, cross AZ or cross region. Applications must update the connection string to leverage read replicas.

Replication is **async**, so reads are eventually consistent. Replicas can be promoted to their own database.

**Read Replicas Use Cases**:

- Having a production database that is taking on normal load.
- Want to run a reporting application to run some analytics.
- To run the new workload.
- To not affect production application.

Read replicas are used only for **SELECT** statements in queries.

In AWS there is a network cost when data goes from one AZ to another. For RDS Read Replicas within the same region, we don't pay that fee.

## Exam tasks
- [[Task 2.1 Design scalable and loosely coupled architectures]]
- [[Task 3.3 Determine high-performing database solutions]]
- [[Task 4.3 Design cost-optimized database solutions]]

---
**Up:** [[Amazon RDS]] · **Map:** [[Database Map]]
