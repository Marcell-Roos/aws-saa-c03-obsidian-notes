---
tags: [topic, cat/database, scope/in]
aliases: ["Amazon DynamoDB", "DynamoDB", "DynamoDB Accelerator", "DAX", "DynamoDB Backups and S3 Integration", "DynamoDB Global Tables", "DynamoDB Indexes and Transactions", "GSI", "LSI", "DynamoDB Streams", "DynamoDB TTL", "Drill DynamoDB"]
---

# DynamoDB

> [!info] Why this matters
> DynamoDB is the default database of serverless designs on AWS. Expect questions on capacity modes, indexes, DAX, global tables and streams, and on when not to use it.
>
> **Covers:** [[Domain 3 Design High-Performing Architectures#Task 3.3|Task 3.3]], [[Domain 4 Design Cost-Optimized Architectures#Task 4.3|Task 4.3]].
> **Study time:** about 2.5 hours.

## What it is

**Amazon DynamoDB** is a fully managed, serverless NoSQL key-value and document database.

- It delivers single-digit millisecond latency at any scale.
- Data is replicated across three AZs automatically.
- There are no servers to manage, and no patching or maintenance windows.
- It is integrated with IAM for access control.
- It has a flexible schema, so items in a table can have different attributes.

It is designed to avoid joins, and supports only a subset of PartiQL. If a workload needs relational queries, use RDS or Aurora.

## Data model

| Term | Meaning |
| --- | --- |
| **Table** | A collection of items |
| **Item** | A row. Up to **400 KB** |
| **Attribute** | A field in an item |
| **Partition key** | Decides which partition stores the item, through a hash |
| **Sort key** | Optional. Orders items that share a partition key |

A **primary key** is either a partition key alone, or a partition key plus a sort key. Without a sort key, no two items can share a partition key.

Choose a **high-cardinality partition key**, one with many distinct values such as `user_id`. A low-cardinality key, such as `status`, sends most traffic to a few partitions. This is a **hot partition**, and it leads to throttling even when the table has spare capacity. A single partition supports up to about 3,000 read units and 1,000 write units per second.

## Capacity modes

| | On-demand | Provisioned |
| --- | --- | --- |
| How it works | Pay per request. Scales automatically | You set read and write capacity units |
| Scaling | Automatic | Optional auto scaling |
| Best for | Unknown or spiky traffic. Now the default, recommended for most workloads | Steady, predictable traffic, where it can be cheaper |

You can switch between modes.

Two **table classes** are available. **DynamoDB Standard** is the default. **Standard-IA** lowers storage cost, with higher request cost, for tables that are mostly stored data and rarely read.

### Calculating capacity

| Unit | Gives you |
| --- | --- |
| **1 RCU** | One strongly consistent read per second of up to 4 KB, or two eventually consistent reads |
| **1 WCU** | One write per second of up to 1 KB |

Item sizes round **up**: to the next 4 KB for reads, and the next 1 KB for writes.

> [!example] Worked examples
> **Read:** 10 strongly consistent reads per second of 6 KB items. 6 KB rounds up to 8 KB, which is 2 RCU per read. Total: 20 RCU.
> **Eventually consistent:** the same reads need half that: 10 RCU.
> **Write:** 10 writes per second of 1.5 KB items. 1.5 KB rounds up to 2 KB, which is 2 WCU per write. Total: 20 WCU.
> **Transactional:** double the normal cost, so 40 RCU or 40 WCU in the examples above.

## Read consistency

| | Eventually consistent | Strongly consistent |
| --- | --- | --- |
| Result | May miss a very recent write | Always returns the latest data |
| Cost | Half | Full |
| Default | Yes | Must be requested |
| Available on | Tables, LSIs, GSIs | Tables and LSIs. **Not GSIs** |

## Reading and writing efficiently

| | Query | Scan |
| --- | --- | --- |
| Reads | Items with one partition key, and optionally a sort key range | **The whole table** |
| Efficiency | High | Low, and costly on big tables |
| Filter expression | Applied after reading | Applied after reading, so you still pay for all items read |

Design tables and indexes so that your application can use Query. If a question describes a Scan causing throttling, the answer is usually a new GSI.

- **Projection expressions** return only the attributes you need, which reduces data transferred, but not capacity consumed.
- **Batch operations** (`BatchGetItem`, `BatchWriteItem`) group requests for efficiency.
- **Conditional writes** succeed only if a condition is true. They give optimistic locking, so that two users cannot overwrite each other's change.
- **Adaptive capacity** shifts unused throughput towards busy partitions automatically, but it does not remove the need for a good partition key.

## Indexes

Indexes let you query on attributes other than the primary key. Without them, you would have to scan the whole table, which is slow and expensive.

| | Global secondary index (GSI) | Local secondary index (LSI) |
| --- | --- | --- |
| Key | Different partition key and sort key | **Same** partition key, different sort key |
| Created | **Any time** | **Only at table creation** |
| Capacity | Its own | Shares the table's |
| Consistency | Eventual only | Eventual or strong |
| Limit per table | 20 | 5 |

"A table keyed on `user_id` must also be queried by `email`" means a GSI. An LSI cannot be added to an existing table, which is a classic trap.

## Transactions

**Transactions** give all-or-nothing reads and writes across multiple items and tables, with ACID guarantees. They cost **twice** the capacity units. Use them for tasks like debiting one account and crediting another.

## DynamoDB Accelerator

**DAX** is a fully managed in-memory cache for DynamoDB.

- It reduces read latency from milliseconds to **microseconds**.
- It is API-compatible, so it needs **no application logic changes**, only a change of client.
- The default cache TTL is 5 minutes.

| | DAX | ElastiCache |
| --- | --- | --- |
| Works with | DynamoDB only | Any data source |
| Caches | Individual items and query results | Anything, such as computed results |
| Code changes | Minimal | Needed |

## DynamoDB Streams

**DynamoDB Streams** is an ordered record of item-level changes: creates, updates and deletes. Records are kept for **24 hours**.

Use it to react to changes in real time, usually with **Lambda triggers**: send a welcome email when a user is added, or update a search index in OpenSearch.

| | DynamoDB Streams | Kinesis Data Streams for DynamoDB |
| --- | --- | --- |
| Retention | 24 hours | Up to 365 days |
| Consumers | Limited | Many |
| Processing | Lambda, the Kinesis adapter | Lambda, Firehose, Flink, Glue |

Replay of last month's changes needs Kinesis, not Streams.

## Global tables

**Global tables** replicate a table across Regions with **active-active** access: applications read and write in any Region, and DynamoDB handles replication.

| Consistency mode | Meaning |
| --- | --- |
| **Multi-Region eventual (MREC)** | The default. Writes replicate asynchronously, usually within seconds |
| **Multi-Region strong (MRSC)** | Writes replicate synchronously, and strongly consistent reads return the latest write in any Region. It needs exactly three Regions: three replicas, or two replicas and a witness |

Older guides say you must enable Streams first. That is no longer something you set up yourself.

The difference from Aurora Global Database: **DynamoDB global tables are multi-writer, and Aurora Global has one writer Region.**

## Time to live

**TTL** deletes items automatically after an expiry timestamp that you store in an attribute. Deletion consumes no write capacity in the Region where it happens (replicated deletes in global table replicas are charged), but it is not immediate. AWS says that items are typically deleted within a few days of expiry, and older material says 48 hours. Filter expired items out of reads if timing matters.

Use it for session data, temporary records and regulatory deletion. Deleted items appear in Streams, so you can archive them to S3.

## Backups and S3 integration

| Feature | Detail |
| --- | --- |
| **Point-in-time recovery (PITR)** | Continuous, optional, 1 to 35 days. Restores to a new table |
| **On-demand backups** | Full backups, kept until deleted. No performance impact. Can be managed through AWS Backup. Restores to a new table |
| **Export to S3** | Needs PITR. Works for any point in the window, and uses no read capacity. Then analyse with Athena |
| **Import from S3** | CSV, DynamoDB JSON or Ion. Creates a new table, and uses no write capacity |

## Security

- Access is controlled by IAM, with fine-grained conditions such as `dynamodb:LeadingKeys`.
- Data is encrypted at rest by default.
- A **gateway VPC endpoint** gives private, free access from a VPC. An interface endpoint also exists, at a cost, and that is the one on-premises networks can reach.

## Design patterns

- **Large objects:** store the file in S3, and keep a pointer plus metadata in DynamoDB, because of the 400 KB limit.
- **Session store:** use a TTL on session items. This makes the web tier stateless.
- **Serverless API:** API Gateway, then Lambda, then DynamoDB.
- **Search:** Streams to Lambda to OpenSearch, because DynamoDB cannot do fuzzy text search.

## Exam patterns

| If the question says | Think | Why |
| --- | --- | --- |
| Spiky or unknown traffic, table throttles | On-demand mode | Pay per request |
| Steady, predictable traffic, lowest cost | Provisioned with auto scaling | |
| Throttling with spare capacity | Hot partition | Better partition key |
| Reads in microseconds, no code rewrite | DAX | API compatible |
| Low-latency reads and writes in every Region | Global tables | Active-active |
| Run logic when items change | Streams with Lambda | |
| Remove old session records automatically and free | TTL | |
| Also query by another attribute, existing table | GSI | LSI only at creation |
| Debit and credit, both or neither | Transactions | Twice the capacity |
| Store 2 MB documents | S3 plus a pointer | 400 KB limit |
| Must see the latest write | Strongly consistent read | Not on a GSI |
| Reporting needs many joins | RDS, Aurora or Redshift | DynamoDB models data to avoid joins |
| Recover to any second in 35 days | PITR | New table |
| Analyse a table without affecting it | Export to S3, then Athena | |
| Replay changes from weeks ago | Kinesis Data Streams | Streams keeps 24 hours |
| Fuzzy text search over table data | OpenSearch | Through Streams |

## Check yourself

**1.** A flash-sale site has traffic that jumps without warning, and its table is throttled during peaks. The team does not want to manage capacity. What should it do?

- A. Use on-demand capacity mode
- B. Add an LSI
- C. Increase item size
- D. Use eventually consistent reads only

> [!success]- Answer
> **A.** On-demand absorbs unpredictable traffic with no capacity planning.

**2.** An application needs microsecond read latency from DynamoDB, with minimal code changes. What should it use?

- A. ElastiCache
- B. DAX
- C. Read replicas
- D. Global tables

> [!success]- Answer
> **B.** DAX is API-compatible with DynamoDB.

**3.** A table is keyed on `order_id`. A new feature must query orders by `customer_id`. The table has been live for a year. What should the team add?

- A. A local secondary index
- B. A global secondary index
- C. A second table in another Region
- D. DAX

> [!success]- Answer
> **B.** A GSI can use a new partition key and can be added at any time. An LSI needs the same partition key and must be created with the table.

**4.** How many RCUs are needed for 20 strongly consistent reads per second of 9 KB items?

- A. 20
- B. 30
- C. 60
- D. 90

> [!success]- Answer
> **C.** 9 KB rounds up to 12 KB, which is 3 RCU per read. Then 3 × 20 = 60.

**5.** How many WCUs are needed for 15 writes per second of 2.5 KB items?

- A. 15
- B. 30
- C. 45
- D. 60

> [!success]- Answer
> **C.** 2.5 KB rounds up to 3 KB, which is 3 WCU per write. Then 3 × 15 = 45.

**6.** Each time a customer record changes, a downstream system must be updated. The team prefers a serverless design. What is the best approach?

- A. Poll the table every minute from EC2
- B. Enable DynamoDB Streams with a Lambda trigger
- C. Export to S3 hourly
- D. Use DAX

> [!success]- Answer
> **B.** Streams with Lambda react to item-level changes in near real time.

**7.** A global application must let users in any Region write with low latency. Which feature fits?

- A. Aurora Global Database
- B. DynamoDB global tables
- C. Cross-Region read replicas
- D. DAX

> [!success]- Answer
> **B.** Global tables are active-active. Aurora Global has one writer Region.

**8.** An application stores user sessions in DynamoDB. Sessions must disappear 30 minutes after creation, at no extra charge. What should it use?

- A. A Lambda function that scans and deletes
- B. TTL on an expiry attribute
- C. On-demand backups
- D. Streams

> [!success]- Answer
> **B.** TTL deletes expired items for free. Deletion can lag, so the app should also check expiry if timing is critical.

**9.** A table shows throttling on some requests, while the total consumed capacity is well under the provisioned level. The partition key is `country`, and most users are in one country. What is the cause?

- A. A hot partition
- B. Too many GSIs
- C. TTL is enabled
- D. PITR is enabled

> [!success]- Answer
> **A.** Low-cardinality keys concentrate traffic on one partition. A key with more distinct values spreads it.

**10.** An application needs to store images of up to 3 MB with metadata that can be queried. What is the recommended design?

- A. Store images as binary attributes in DynamoDB
- B. Store images in S3, and metadata plus the S3 key in DynamoDB
- C. Store images on instance store
- D. Compress them to fit into 400 KB

> [!success]- Answer
> **B.** Items are limited to 400 KB, and S3 is designed for objects.

---
**Previous:** [[13 RDS and Aurora]] · **Next:** [[15 ElastiCache and Other Databases]] · **Plan:** [[Study Guide]]
