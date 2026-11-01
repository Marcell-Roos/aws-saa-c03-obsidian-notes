---
tags: [service, cat/management, scope/in]
aliases: ["Logs Insights", "CloudWatch Logs Insights"]
---

# CloudWatch Logs

**CloudWatch Logs** is a logging service that monitors, stores, and access log files from AWS resources, applications, and services. Logs are encrypted by default.

- Log groups - arbitrary name, usually representing an application.
- Log stream - instance within applications/log files/containers.

CloudWatch Logs can send logs to: [[Amazon S3|S3]], [[Kinesis Data Streams|KDS]], [[Amazon Data Firehose|KDF]], [[AWS Lambda]], [[Amazon OpenSearch Service|OpenSearch]].

Logs can be collected from: [[AWS Elastic Beanstalk|Elastic Beanstalk]], [[Amazon ECS|ECS]], AWS Lambda, [[AWS CloudTrail|CloudTrail]], [[Amazon CloudWatch|CloudWatch]] Log agents (on [[Amazon EC2|EC2 instances]] or on-premises servers), [[Amazon Route 53|Route53]].

**CloudWatch Logs Insights** - search and analyze log data stored in CloudWatch Logs. Provides a [[Purpose-Built Databases|purpose-built]] query language. It automatically discovers fields from AWS services and JSON log events. We can save queries and add them to CloudWatch Dashboard. It’s query engine, not a real-time engine.

Log data can take up to 12h to become available for export. It is not near real-time or real-time, if we want that we should use Logs Subscriptions instead.

**CloudWatch Logs Subscriptions** - lets us get a real-time log events from CloudWatch Logs for processing and analysis. We can send to KDS, KDF or AWS Lambda. There is Subscription Filter which can filter which logs will be delivered to our destination.

We can have Cross-Account Subscription which can send log events to resources in different AWS account (KDS, KDF).

- **Solution Architecture - Logs Aggregation (Multi-Account & Multi Region).** Subscription filters in each account send logs to a destination in a central account, usually through Kinesis Data Streams and Firehose into S3.

---
**Up:** [[Amazon CloudWatch]] · **Map:** [[Management and Governance Map]]
