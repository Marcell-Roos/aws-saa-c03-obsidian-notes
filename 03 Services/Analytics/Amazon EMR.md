---
tags: [service, cat/analytics, scope/in]
aliases: ["EMR"]
---

# Amazon EMR

**EMR** helps creating Hadoop clusters (Big Data) to analyze and process vast amount of data. The clusters can be made of hundreds of [[Amazon EC2|EC2 instances]]. It takes care of all the provisioning and configuration. It has auto-scaling and it’s integrated with [[EC2 Spot Instances|Spot instances]].

EMR supports Apache Spark, HBase, Presto, Flink…

Usage: data processing, log analysis, ML, web indexing, big data …

**EMR Node Types**

- **Primary Node** (formerly master) - manages and coordinates the cluster (long running).
- **Core Node** - runs tasks and stores data (long running).
- **Task Node** (optional) - just to run tasks (short running).

**EMR Cluster Types**

- **Long-running Cluster** - designed for ongoing data processing needs. They remain active for extended periods, allowing users to submit multiple jobs over time without the overhead of cluster startup and configuration.
- **Transient Cluster** - designed for short-lived, one-off jobs. They are created for specific processing tasks and terminated immediately after the job is complete.

**Purchasing Options**

- **On-demand** - reliable, predictable, won't be terminated.
- **Reserved** (min 1 year) - cost savings (EMR will automatically use if available).
- **Spot Instances** - cheaper, can be terminated, less reliable.
- **Solution Architecture - Process Data from an On-Premises Database.** Use [[AWS DMS|DMS]] or [[AWS Direct Connect|Direct Connect]] to bring data into [[Amazon S3|S3]], process it on a transient EMR cluster with Spot task nodes, then load results into S3 or [[Amazon Redshift|Redshift]].

## Exam tasks
- [[Task 3.2 Design high-performing and elastic compute solutions]]
- [[Task 3.5 Determine high-performing data ingestion and transformation solutions]]

---
**Map:** [[Analytics Map]]
