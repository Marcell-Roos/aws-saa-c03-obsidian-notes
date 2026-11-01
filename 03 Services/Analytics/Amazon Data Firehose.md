---
tags: [service, cat/analytics, scope/in]
aliases: ["Firehose", "Kinesis Data Firehose", "KDF"]
---

# Amazon Data Firehose

**KDF** is a fully managed service that makes it easy to reliably load streaming data into [[Data Lakes|data lakes]], data stores, and analytics services. We pay for data going through Firehose.

It supports many data formats, conversions, transformations and compression. It supports custom data transformations using [[AWS Lambda]]. Firehose can send failed or all data to a backup [[Amazon S3|S3 bucket]].

Because we write data in batches, KDF is near real time. If we set buffer interval to zero seconds (no buffering) it will be still considered near real time.

Formerly Kinesis Data Firehose. Destinations include S3, [[Amazon Redshift|Redshift]], [[Amazon OpenSearch Service|OpenSearch]], Splunk, Apache Iceberg tables and HTTP endpoints. It can convert records to [[Data Formats|Parquet]].

## Exam tasks
- [[Task 3.5 Determine high-performing data ingestion and transformation solutions]]

---
**Up:** [[Amazon Kinesis]] · **Map:** [[Analytics Map]]
