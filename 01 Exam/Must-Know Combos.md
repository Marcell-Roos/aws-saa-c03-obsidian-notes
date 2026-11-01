---
tags: [exam, scope/in]
---

# Must-Know Combos

| Need | Combo |
| --- | --- |
| Serverless web app | [[Amazon CloudFront\|CloudFront]], [[Amazon S3\|S3]], [[Amazon API Gateway\|API Gateway]], [[AWS Lambda\|Lambda]], [[Amazon DynamoDB\|DynamoDB]] |
| Reliable [[SNS and SQS Fan-Out\|fan-out]] | [[Amazon SNS\|SNS]] to multiple [[Amazon SQS\|SQS]] queues |
| Global database | [[Aurora Global Database]] (SQL) or [[DynamoDB Global Tables]] (NoSQL) |
| Protect a web app | CloudFront, [[AWS WAF\|WAF]], Shield, [[Application Load Balancer\|ALB]] |
| Real-time pipeline | [[Kinesis Data Streams]], Lambda, then DynamoDB or S3 |
| Data lake analytics | S3, [[AWS Glue\|Glue]], Athena, Amazon Quick |
| Migration toolkit | DataSync for files, DMS for databases, Direct Connect for transport |
| DR stack | Route 53 failover, Aurora Global Database, S3 Cross-Region Replication |
| App sign-in | Cognito user pools for login, identity pools for AWS credentials |

See [[Architecture Patterns]].

---
**Up:** [[SAA-C03 Exam Overview]]
