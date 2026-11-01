---
tags: [service, cat/database, scope/in]
aliases: ["GSI", "LSI", "Global Secondary Index", "Local Secondary Index"]
---

# DynamoDB Indexes and Transactions

| | GSI | LSI |
| --- | --- | --- |
| Key | Different partition and sort key | Same [[Data Ordering in Kinesis and SQS FIFO\|partition key]], different sort key |
| Created | Any time | Only at table creation |
| Capacity | Its own | Shares the table's |
| Consistency | Eventual only | Eventual or strong |

**Primary key:** either a partition key alone, or a partition key plus a sort key. Choose a high-cardinality partition key to avoid hot partitions.

**Transactions** give all-or-nothing reads and writes across items and tables, and cost twice the capacity units.

**[[DynamoDB Accelerator|DAX]] vs [[Amazon ElastiCache|ElastiCache]]:** [[DynamoDB Accelerator]] caches [[Amazon DynamoDB|DynamoDB]] items with no code changes. [[Amazon ElastiCache]] suits computed results and needs code changes.

---
**Up:** [[Amazon DynamoDB]] · **Map:** [[Database Map]]
