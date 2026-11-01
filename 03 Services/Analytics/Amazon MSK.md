---
tags: [service, cat/analytics, scope/in]
aliases: ["MSK"]
---

# Amazon MSK

**MSK** is an alternative to [[Amazon Kinesis]]. It is fully managed Apache Kafka on AWS. It allows us to create, update and delete clusters.

MSK creates and manages Kafka broker nodes and the metadata layer for us (KRaft controllers on newer clusters, ZooKeeper nodes on older ones). We can deploy the MSK cluster in our [[Amazon VPC|VPC]] and multi-AZ. Data is stored in **[[Amazon EBS|EBS]]** volumes for as long as we want.

**MSK Serverless** - run Apache Kafka on MSK without managing the capacity.

**MSK Consumers**

Consumers include [[Managed Service for Apache Flink]], [[AWS Glue|Glue]] streaming ETL, [[AWS Lambda|Lambda]], and applications on [[Amazon EC2|EC2]], [[Amazon ECS|ECS]] or [[Amazon EKS|EKS]].

See [[Kinesis Data Streams vs Amazon MSK]].

## Exam tasks
- [[Task 3.5 Determine high-performing data ingestion and transformation solutions]]

---
**Map:** [[Analytics Map]]
