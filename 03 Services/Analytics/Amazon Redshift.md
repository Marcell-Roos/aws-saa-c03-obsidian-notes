---
tags: [service, cat/analytics, scope/in]
aliases: ["Redshift", "Redshift Spectrum"]
---

# Amazon Redshift

**Redshift** is based on Postgres, but it’s not used for [[OLTP and OLAP|OLTP]] (Online Transaction Processing). It is used for **OLAP** (Online Analytical Processing - Analytics & Data Warehousing). Data is loaded in batches rather than row by row. AWS quotes up to 10x better performance than other data warehouses, and it scales to PBs of data. Has Massively Parallel Processing (MPP), highly available.

Instead of row based storage of data Redshift uses columns. Compared with [[Amazon Athena|Athena]], Redshift is faster for complex queries, joins and aggregations because data is loaded into columnar storage and organised with sort and distribution keys. It has no traditional indexes.

Redshift has pay as you go type of pricing based on the instances provisioned. By leveraging **cross-region snapshot copying**, we can significantly enhance our Redshift cluster’s resilience and ensure that our data is protected against regional disruptions.

**Redshift Cluster**

- **Leader Node** - for query planning and results aggregation.
- **Compute Node** - for performing the queries and sending results to leader.

On a provisioned cluster we choose the node size in advance and can use [[EC2 Reserved Instances|Reserved Instances]] for savings. Redshift Serverless removes that step.

**Redshift Spectrum** - feature which lets us query data that is already in [[Amazon S3|S3]] without loading it. For this we must have a Redshift cluster available to start the query.

**Redshift Snapshots & DR**

Redshift has Multi-AZ mode for some clusters. Snapshots are PIT backups of a cluster, stored internally in S3. They are incremental (only what has changed is saved). We can restore a snapshot into a new cluster.

- **Automated snapshots** - every 8h, every 5GB or on a schedule. Need to set retention period.
- **Manual snapshots** - snapshot is retained until we delete it.

We can configure Redshift to automatically copy snapshots of a cluster to another AWS Region.

**Loading Data into Redshift**

Use Data [[Amazon Data Firehose|Firehose]] (through S3 and COPY), the COPY command from S3, or JDBC inserts from [[Amazon EC2|EC2]]. Large batches are much better than small ones.

**Redshift Serverless** runs without clusters. **Zero-ETL** integrations load data from [[Amazon Aurora|Aurora]] and other sources without pipelines.

## In this topic
- [[Redshift Performance Features]]

## Exam tasks
- [[Task 3.5 Determine high-performing data ingestion and transformation solutions]]
- [[Task 4.3 Design cost-optimized database solutions]]

---
**Map:** [[Analytics Map]]
