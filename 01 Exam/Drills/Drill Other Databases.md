---
tags: [drill, scope/in]
---

# Drill Other Databases

Adapted from [RonitSachdev/aws-saa-c03-guides](https://github.com/RonitSachdev/aws-saa-c03-guides) (CC BY 4.0), with outdated facts changed.

## Question patterns

- *"BI team needs a petabyte-scale data warehouse for complex analytical queries"* → **[[Amazon Redshift|Redshift]]** ([[OLTP and OLAP|OLAP]], columnar, built for BI)
- *"Query data in [[Amazon S3|S3]] from the existing Redshift cluster without loading it"* → **Redshift Spectrum** (extends the warehouse into S3)
- *"Run occasional SQL queries on [[Application Load Balancer|ALB]]/VPC logs stored in S3, minimal setup"* → **[[Amazon Athena|Athena]]** (serverless SQL-on-S3)
- *"Reduce Athena costs and speed up queries"* → **[[Data Formats|Parquet]]/ORC + compression + partitioning** (bill = TB scanned, so scan less)
- *"Social app needs friend-of-friend recommendations / detect fraud rings"* → **[[Amazon Neptune|Neptune]]** (relationships = graph)
- *"Millions of IoT sensor readings per minute, analyzed over time windows"* → **[[Amazon Timestream|Timestream]]** (time-series)
- *"Migrate a MongoDB workload to a managed AWS service"* → **[[Amazon DocumentDB|DocumentDB]]** (keyword match, done)
- *"Migrate a Cassandra workload"* → **[[Amazon Keyspaces|Keyspaces]]** (keyword match, done)
- *"Product catalog needs fuzzy, typo-tolerant full-text search; data is in [[Amazon DynamoDB|DynamoDB]]"* → **[[Amazon OpenSearch Service|OpenSearch]]** (via [[DynamoDB Streams]] → [[AWS Lambda|Lambda]]; DynamoDB can't fuzzy-search)
- *"Analysts' reports are slowing the production OLTP database"* → **move analytics off prod** — to Redshift (the cardinal sin, corrected)

## Pocket card

| Keyword | Answer |
|---|---|
| Data warehouse / OLAP / BI / petabyte | Redshift |
| Query S3 from Redshift, no loading | Redshift Spectrum |
| SQL on S3, serverless, ad-hoc / logs | Athena |
| Cut Athena cost | Parquet/ORC + compress + partition |
| Graph / social / fraud ring / recommendations | Neptune |
| Time-series / IoT / telemetry / metrics | Timestream |
| "MongoDB" | DocumentDB |
| "Cassandra" | Keyspaces |
| Full-text / fuzzy search, log dashboards | OpenSearch |
| Analytics choking prod OLTP DB | Move it — Redshift |

---
**Up:** [[Drills Map]]
