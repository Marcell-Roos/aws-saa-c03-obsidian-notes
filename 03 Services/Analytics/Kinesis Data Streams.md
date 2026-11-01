---
tags: [service, cat/analytics, scope/in]
aliases: ["KDS"]
---

# Kinesis Data Streams

**KDS** is a real-time data streaming service designed to handle massive streams of data in real-time. We have ability to reprocess data. Records are immutable: they can't be deleted individually and expire when the retention period ends (24 hours by default, up to 365 days).

**Key Concepts**

- **Stream** - a collection of records that are distributed across multiple shards. Each stream has a sequence of data records.
- **Shard** - the fundamental unit of capacity within a stream. A stream can have multiple shards, allowing for scaling up.
- **Record** - a unit of data in a stream. It consists of:
    - Data Blob - data we want to store.
    - [[Data Ordering in Kinesis and SQS FIFO|Partition Key]] - string used to group records by shard within a stream.
    - Sequence Number - an identifier assigned to each record, unique per shard, that is used to maintain order.
- **Producers** - clients or services that write data to the KDS (AWS SDK, KPL, [[Amazon Kinesis|Kinesis]] Agent).
- **Consumers** - applications or services that process or consume the data (AWS SDK, KCL, [[AWS Lambda]], [[Amazon Data Firehose|KDF]], [[Managed Service for Apache Flink|KDA]]).

**KDS Capacity Modes**

- **Provisioned mode** - we choose the number of shards provisioned, scale manually or using API. We pay per shard provisioned per hour.
- **On-demand mode** - no need to provision or manage the capacity. Scales automatically based on observed throughput peak during the last 30 days. We pay per stream per hour & data in/out per GB.

**KDS Security**

We can control access/authorization using [[IAM Policy Structure|IAM policies]]. Encryption in flight is done using HTTPS endpoints and at rest using [[AWS KMS|KMS]]. Also we can implement encryption/decryption of data on client side.

We can use [[VPC Endpoints]] for Kinesis to access within [[Amazon VPC|VPC]]. To monitor API calls we use [[AWS CloudTrail|CloudTrail]].

**Capacity:** each provisioned shard takes 1 MB/s in and gives 2 MB/s out. **Record size:** up to 10 MiB. **Retention:** 24 hours by default, up to 365 days. **Enhanced [[SNS and SQS Fan-Out|fan-out]]** gives each consumer dedicated throughput.

## Exam tasks
- [[Task 3.5 Determine high-performing data ingestion and transformation solutions]]

---
**Up:** [[Amazon Kinesis]] · **Map:** [[Analytics Map]]
