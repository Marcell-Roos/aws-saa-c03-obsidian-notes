---
tags: [service, cat/database, scope/in]
aliases: ["RDS"]
---

# Amazon RDS

**RDS** is a managed DB service which uses SQL as a query language. It allows us to create databases in the cloud that are managed by AWS (Postgres, MySQL, MariaDB, Oracle, Microsoft SQL Server, IBM Db2, [[Amazon Aurora|Aurora]]).

RDS is a managed service:

- Automated provisioning, OS patching.
- Continous backups and restore to a specific timestamp (Point in Time Restore).
- Dashboards monitoring.
- Read replicas for improved read performance.
- Multi AZ setup for [[Disaster Recovery Strategies|disaster recovery]].
- Maintenance windows for upgrades.
- Vertical and [[Scalability and High Availability|horizontal scaling]] capability.
- Storage backed by [[Amazon EBS|EBS]].

We can't SSH into our RDS instances.

**RDS Storage Auto Scaling** helps us increase storage on our RDS instance dynamically. When RDS detects we are running out of free database storage, it scales automatically. We have to set maximum storage threshold. It is useful for applications with unpredictable workloads.

It automatically modifies storage if:

- Free storage is less than 10% of allocated storage.
- Low-storage lasts at least 5 minutes.
- 6 hours have passed since last modifications.

- Managed Postgres/MySQL/Oracle/SQL Server/DB2/MariaDB/Custom.
- Provisioned RDS instance size & EBS Volume type & size.
- Auto scaling capability for storage.
- Support for [[RDS Read Replicas|Read Replicas]] & Multi-AZ.
- Security through [[AWS IAM|IAM]], [[Security Groups]], [[AWS KMS|KMS]], SSL in transit.
- Automated backup with [[DynamoDB Backups and S3 Integration|PITR]] (35 days).
- Manual DB Snapshots for longer-term recovery.
- Managed and scheduled maintenance (with downtime).
- Support for IAM authentication, integration with [[AWS Secrets Manager|Secrets Manager]].
- [[RDS Custom]] for access to and customize the underlying instance (Oracle & SQL Server).
- Used for RDBMS & [[OLTP and OLAP|OLTP]].

For a stopped or short-lived dev database, snapshot and delete it to save costs. See [[RDS Multi-AZ vs Read Replicas vs Aurora Global]].

## In this topic
- [[RDS Blue-Green Deployments]]
- [[RDS Custom]]
- [[RDS Lambda Invocation and Event Notifications]]
- [[RDS Monitoring]]
- [[RDS Multi-AZ]]
- [[RDS Proxy]]
- [[RDS Read Replicas]]
- [[RDS and Aurora Backups]]
- [[RDS and Aurora Restore and Cloning]]
- [[RDS and Aurora Security]]

## Exam tasks
- [[Task 3.3 Determine high-performing database solutions]]
- [[Task 4.3 Design cost-optimized database solutions]]

---
**Map:** [[Database Map]]
