---
tags: [service, cat/analytics, scope/in]
aliases: ["Glue", "Glue Data Catalog"]
---

# AWS Glue

**AWS Glue** is a serverless fully managed extract, transform, and load (**ETL**) service. It is useful for preparing and transforming data for analytics.

**Glue Components**

- **Data Catalog** - central repository that stores metadata about datasets in our AWS environment. Can be used by [[Amazon Athena|Athena]], [[Amazon Redshift|Redshift]] or [[Amazon EMR|EMR]].
- **ETL Engine** - automatically generates Python or Scala code to extract data from various sources, transform it, and load it into target data stores.
- **Crawlers** - automated processes in AWS Glue that scan and infer the schema of data stored in various sources.
- **Glue Jobs** - ETL scripts that users create to transform data. These jobs can be scheduled and monitored within AWS Glue.

**Glue Advanced Features**

**Glue Job Bookmarks** - save and track the data that has already been processed, prevent re-processing old data.

**Glue DataBrew** - clean and normalize data using pre-built transformation.

**Glue Studio** - used to create, run and monitor ETL jobs in Glue.

**Glue Streaming ETL** - run Glue jobs as streaming jobs. compatible with [[Kinesis Data Streams|KDS]], Kafka, [[Amazon MSK|MSK]]

**Glue PySpark Jobs**

PySpark provides distributed processing via Apache Spark, which makes Glue ideal for handling large datasets and complex transformations.

- **Solution Architecture - Convert data into [[Data Formats|Parquet]] format.**

AWS Glue Ray jobs are closed to new customers.

## Exam tasks
- [[Task 3.5 Determine high-performing data ingestion and transformation solutions]]

---
**Map:** [[Analytics Map]]
