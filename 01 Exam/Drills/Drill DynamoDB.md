---
tags: [drill, scope/in]
---

# Drill DynamoDB

Adapted from [RonitSachdev/aws-saa-c03-guides](https://github.com/RonitSachdev/aws-saa-c03-guides) (CC BY 4.0), with outdated facts changed.

## Question patterns

- *"Flash sale causes unpredictable spikes; table throttles"* → **On-Demand capacity mode** (pay-per-request absorbs spikes)
- *"Reduce read latency to microseconds without changing application code"* → **[[DynamoDB Accelerator|DAX]]** (API-compatible cache, DynamoDB-only)
- *"Global users need low-latency reads AND writes in every region"* → **[[DynamoDB Global Tables|Global Tables]]** (active-active; [[Aurora Global Database|Aurora Global]] has only one writer)
- *"Run custom logic whenever items are added or modified"* → **[[DynamoDB Streams]] + [[AWS Lambda|Lambda]]** (24-hour change feed triggers functions)
- *"Automatically remove session records after 30 minutes, at no cost"* → **TTL** (free auto-delete, ~48h window)
- *"Table keyed on user_id, but app must also query by email"* → **[[DynamoDB Indexes and Transactions|GSI]]** (new query attribute, addable anytime — LSI is creation-time-only bait)
- *"Debit one account and credit another — both or neither"* → **[[Amazon DynamoDB|DynamoDB]] Transactions** (ACID, 2x capacity cost)
- *"Store 2 MB documents per record"* → **[[Amazon S3|S3]] for the object, DynamoDB holds the pointer** (400 KB item limit)
- *"Application must always see the most recent write"* → **Strongly consistent read** (1 RCU vs 2 eventual reads)
- *"Reporting needs joins across many tables"* → **[[Amazon RDS|RDS]]/Aurora**, not DynamoDB (relational = SQL)

## Pocket card

| Keyword | Answer |
|---|---|
| Serverless NoSQL, key-value, any scale | DynamoDB |
| Joins / complex SQL | RDS or [[Amazon Aurora\|Aurora]] instead |
| Spiky / unknown traffic | On-Demand mode |
| Steady, predictable traffic | Provisioned (+ auto scaling) |
| Microseconds, no code change | DAX |
| Multi-region active-active | Global Tables (needs Streams) |
| React to item changes | Streams → Lambda |
| Auto-expire items free | TTL |
| Query by another attribute, existing table | GSI (LSI = creation-time trap) |
| Atomic multi-item | Transactions (2x cost) |
| Restore to any second, 35 days | [[DynamoDB Backups and S3 Integration\|PITR]] |
| Item > 400 KB | S3 + pointer |
| 1 RCU | 1 strong or 2 eventual reads ≤ 4 KB |
| 1 WCU | 1 write ≤ 1 KB |

---
**Up:** [[Drills Map]]
