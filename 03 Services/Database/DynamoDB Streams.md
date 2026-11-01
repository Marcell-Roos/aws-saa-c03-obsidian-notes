---
tags: [service, cat/database, scope/in]
---

# DynamoDB Streams

**[[Amazon DynamoDB|DynamoDB]] Stream Processing** - ordered stream of item-level modifications (create/update/delete) in a table.

It is used for reacting to changes in real time, real time usage analytics, implementing cross-region replication, invoke [[AWS Lambda]] on changes to our DynamoDB table…

- **DynamoDB Streams** - process using AWS Lambda Triggers or DynamoDB Stream [[Amazon Kinesis|Kinesis]] adapter. We have 24h retention and it has limited number of consumers.
- **[[Kinesis Data Streams|KDS]]** - Process using AWS Lambda, [[Managed Service for Apache Flink|KDA]], [[Amazon Data Firehose|KDF]], [[AWS Glue]] Streaming ETL… We have 1 year retention and it has high number of consumers.

---
**Up:** [[Amazon DynamoDB]] · **Map:** [[Database Map]]
