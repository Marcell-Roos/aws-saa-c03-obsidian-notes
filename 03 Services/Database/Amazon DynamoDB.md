---
tags: [service, cat/database, scope/in]
aliases: ["DynamoDB"]
---

# Amazon DynamoDB

**DynamoDB** is fully managed and highly available NoSQL schemaless database with replication across 3 AZ. It’s distributed serverless database which can scale to massive workloads. DynamoDB is fast and consistent in performance (can handle millions of requests per second, trillions of row and 100s of TB of storage). It’s low cost and has auto scaling capabilities. It can rapidly evolve schemas. It has **single-digit millisecond latency** (low latency retrieval).

DynamoDB is integrated with [[AWS IAM|IAM]] for security, authorization and administration.

DynamoDB uses the **[[Data Ordering in Kinesis and SQS FIFO|partition key]]** value as input to an internal hash function. The output from the hash function determines the partition in which the item will be stored. All items with the same partition key are stored together, in sorted order by sort key value. If no sort key is used, no two items can have the same partition key value.

**Read/Write Capacity Modes**

- **Provisioned Mode** - we specify the number of reads/writes per second and need to plan capacity beforehand. We pay for provisioned Read Capacity Units (RCU) & Write Capacity Units (WCU). It is possible to add auto scaling mode for RCU & WCU.

    The more distinct partition key values that our workload accesses, the more those requests will be spread across the partitioned space.

- **On-demand Mode** (default and recommended for most workloads) - read/writes automatically scale up/down with our workloads. No capacity planning is needed. We pay per request, with no idle capacity to pay for. It is great for unpredictable workloads, steep sudden spikes.

- AWS proprietary technology, managed serverless NoSQL database, millisecond latency.
- Capacity modes: provisioned capacity with optional auto scaling or on-demand capacity.
- Can replace [[Amazon ElastiCache|ElastiCache]] as a key/value store (storing session data for example, using TTL).
- Highly available, Multi-AZ by default, read & writes are decoupled, transaction capability.
- [[DynamoDB Accelerator|DAX]] cluster for read cache, microsecond read latency.
- Security, authentication and authorization is done through IAM.
- Event processing: [[DynamoDB Streams]] to integrate with [[AWS Lambda]] or [[Kinesis Data Streams|KDS]].
- [[DynamoDB Global Tables|Global Table]] feature: active-active setup.
- Automate backups up to 35 days with [[DynamoDB Backups and S3 Integration|PITR]] or on-demand backups.
- Export to [[Amazon S3|S3]] without using RCU within the PITR window, import from S3 without using WCU.
- Great to rapidly evolve schemas.
- Used for serverless applications development and distributed serverless cache.

**Limits:** an item can be up to 400 KB. **Capacity units:** 1 RCU is one strongly consistent read per second of up to 4 KB, or two eventually consistent reads. 1 WCU is one write per second of up to 1 KB.

**Indexes:** a **[[DynamoDB Indexes and Transactions|GSI]]** has a different partition key and can be added at any time. An **LSI** shares the partition key and must be created with the table.

**Transactions** give ACID operations across items and tables.

## In this topic
- [[DynamoDB Accelerator]]
- [[DynamoDB Backups and S3 Integration]]
- [[DynamoDB Global Tables]]
- [[DynamoDB Indexes and Transactions]]
- [[DynamoDB Streams]]
- [[DynamoDB TTL]]

## Exam tasks
- [[Task 3.3 Determine high-performing database solutions]]
- [[Task 4.3 Design cost-optimized database solutions]]

---
**Map:** [[Database Map]]
