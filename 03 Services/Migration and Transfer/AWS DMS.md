---
tags: [service, cat/migration, scope/in]
aliases: ["DMS", "Database Migration Service", "AWS Database Migration Service"]
---

# AWS DMS

With **DMS** we can quickly and securely migrate databases to AWS. The source database remains available during the migration. DMS supports both homogeneous and heterogeneous migrations. It can migrate data from various sources like on-premises databases or other AWS services. DMS includes a schema conversion tool (AWS SCT) that helps convert the schema of source databases to match the target database schema.

- **Homogeneous migrations** - involves moving data between two systems that have the same DBMS.
- **Heterogeneous migrations** - involves moving data between two systems that have different DBMS.

It can be used for continuous data replication with minimal latency (keep source and target databases in sync for ongoing data changes).

When Multi-AZ is enabled, DMS provision and maintains a synchronously stand replica in a different AZ. It eliminates I/O freezes and provides data redundancy.

- **Solution Architecture - [[Amazon S3|S3]] to [[Kinesis Data Streams|KDS]]**

    AWS DMS lets us expand the existing application to stream data from Amazon S3 into [[Amazon Kinesis]] Data Streams for real-time analytics without writing and maintaining new code.

**DMS Serverless** handles capacity, and **DMS Schema Conversion** or the AWS SCT tool handle heterogeneous schema changes. Use SCT or Schema Conversion when engines differ.

## In this topic
- [[DMS Replication Details]]
- [[RDS and Aurora Migrations]]

## Exam tasks
- [[Task 3.3 Determine high-performing database solutions]]
- [[Task 4.3 Design cost-optimized database solutions]]

---
**Map:** [[Migration and Transfer Map]]
