---
tags: [concept, scope/in]
aliases: ["Parquet", "columnar format"]
---

# Data Formats

Row formats such as CSV and JSON are easy to produce but slow to scan. Columnar formats such as **Parquet** and **ORC** compress better and let [[Amazon Athena]] read only the columns needed, which cuts cost.

[[AWS Glue]] jobs or [[Amazon Data Firehose]] record format conversion can change CSV or JSON into Parquet. Partition data in [[Amazon S3|S3]] by date or key to scan less.

## Exam tasks
- [[Task 3.5 Determine high-performing data ingestion and transformation solutions]]

---
**Up:** [[Concepts Map]]
