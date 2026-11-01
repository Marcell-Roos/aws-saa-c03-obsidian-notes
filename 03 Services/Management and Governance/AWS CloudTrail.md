---
tags: [service, cat/management, scope/in]
aliases: ["CloudTrail"]
---

# AWS CloudTrail

**AWS CloudTrail** provides governance, compliance and audit for our AWS account. Event history is on by default for every account and keeps 90 days of management events; to keep events longer we create a **trail**. We can get history of events and API calls made within our account. It’s possible to put logs from CloudTrail into [[CloudWatch Logs]] or [[Amazon S3|S3]]. Can be applied to all regions (default) or a single region. By default, CloudTrail event log files are encrypted using Amazon S3 server-side encryption (SSE).

**CloudTrail Events**

- **Management Events** - operations that are performed on resources in our AWS account. By default, trails are configured to log management events. We can separate read events from write events.
- **Data Events** - S3 object-level activity and [[AWS Lambda|Lambda function]] execution activity (get, delete, put). By default, data events are not logged because high volume operations. It can separate read events from write events.
- **CloudTrail Insights Events**

**CloudTrail Insights** is a feature within AWS CloudTrail that helps us detect unusual or unexpected activity in your AWS accounts. It continuously analyzes our CloudTrail event logs to identify patterns and anomalies, enabling us to quickly respond to potential security issues.

Events are stored for 90 days in CloudTrail. To keep events beyond this period we should log them to S3 and use [[Amazon Athena|Athena]].

- **Solution Architecture - Intercept API Calls (CloudTrail + [[Amazon EventBridge|EventBridge]])**

**Trails** deliver to S3 and can send to CloudWatch Logs. **Log file validation** proves logs weren't changed. An **organization trail** covers every account. CloudTrail Lake closed to new customers on 31 May 2026.

## Exam tasks
- [[Task 1.3 Determine appropriate data security controls]]

---
**Map:** [[Management and Governance Map]]
