---
tags: [service, cat/database, scope/in]
aliases: ["Amazon RDS Proxy"]
---

# RDS Proxy

**RDS Proxy** is a fully managed (serverless, autoscaling, multi-AZ) database proxy for [[Amazon RDS|RDS]]. It allows apps to pool and share database connections established with the database. No code changes are required for most apps to integrate with RDS Proxy.

It improves database efficiency by reducing the stress on database resources and minimizes open connections and timeouts. It reduces RDS & [[Amazon Aurora|Aurora]] failover time by up to 66%.

RDS Proxy can enforce [[AWS IAM|IAM]] authentication for clients and reads database credentials from [[AWS Secrets Manager]].

RDS Proxy is never publicly accessible (must be accessed from [[Amazon VPC|VPC]]).

## Exam tasks
- [[Task 2.2 Design highly available and or or fault-tolerant architectures]]
- [[Task 3.3 Determine high-performing database solutions]]
- [[Task 4.3 Design cost-optimized database solutions]]

---
**Up:** [[Amazon RDS]] · **Map:** [[Database Map]]
