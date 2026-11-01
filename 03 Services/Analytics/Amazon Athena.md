---
tags: [service, cat/analytics, scope/in]
aliases: ["Athena"]
---

# Amazon Athena

**Athena** is a serverless query service which is used to analyze data stored in [[Amazon S3|S3]]. It uses standard SQL to query the files and supports CSV, JSON, ORC, Avro and [[Data Formats|Parquet]]. It is commonly used with [[Amazon Quick|Quicksight]] for reporting/dashboards.

Use cases: business intelligence, analytics, reporting, analyzing querying [[VPC Flow Logs]], [[AWS CloudTrail|CloudTrail]] trails, etc…

**Athena Federated Query** - allows us to run SQL queries across data stored in relational, non-relational, object and custom data sources. It uses Data Source Connectors that run on [[AWS Lambda]] and it stores results back in S3.

**Athena Performance Improvement**

- Use columnar data for cost-savings (less scan) - Apache Parquet or ORC is recommended. We can use [[AWS Glue|Glue]] to convert our data to Parquet or ORC.

- Compress data - for smaller retrievals.
- Partition datasets in S3 - easy querying on virtual columns (*s3://athena-ex/flight/parquet/year=1995/month=1/day=1*).
- Use larger files (> 128MB) to minimize overhead.

## Exam tasks
- [[Task 3.5 Determine high-performing data ingestion and transformation solutions]]

---
**Map:** [[Analytics Map]]
