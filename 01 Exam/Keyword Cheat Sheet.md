---
tags: [exam, scope/in]
---

# Keyword Cheat Sheet

| Words in the question | Think |
| --- | --- |
| Static IP for a [[Elastic Load Balancing\|load balancer]] | [[Network Load Balancer]] |
| Static anycast IPs, TCP or UDP, global | [[AWS Global Accelerator]] |
| Path or host routing | [[Application Load Balancer]] |
| Third-party firewall appliances | [[Gateway Load Balancer]] |
| Too many database connections from [[AWS Lambda\|Lambda]] | [[RDS Proxy]] |
| Read-heavy relational database | [[RDS Read Replicas]] or [[Amazon ElastiCache]] |
| Microsecond [[Amazon DynamoDB\|DynamoDB]] reads | [[DynamoDB Accelerator]] |
| Unknown access pattern on [[Amazon S3\|S3]] | [[S3 Storage Classes]] ([[S3 Storage Classes\|Intelligent-Tiering]]) |
| WORM, even root can't delete | [[S3 Object Lock and Glacier Vault Lock]] (Compliance mode) |
| Sensitive data or PII in S3 | [[Amazon Macie]] |
| Threat detection from logs | [[Amazon GuardDuty]] |
| Vulnerability scanning | [[Amazon Inspector]] |
| Who made this API call | [[AWS CloudTrail]] |
| Resource configuration history and compliance | [[AWS Config]] |
| Metrics, logs and alarms | [[Amazon CloudWatch]] |
| Trace requests across services | [[AWS X-Ray]] |
| Investigate root cause of a security finding | [[Amazon Detective]] |
| Central view of security findings | [[AWS Security Hub]] |
| Compliance reports such as SOC or PCI | [[AWS Artifact]] |
| Share resources between accounts | [[AWS Resource Access Manager]] |
| Hub-and-spoke for many [[Amazon VPC\|VPCs]] | [[AWS Transit Gateway]] |
| Expose a service privately to other VPCs | [[AWS PrivateLink]] |
| Windows SMB shares | [[FSx for Windows File Server]] |
| HPC parallel file system | [[FSx for Lustre]] |
| On-premises access to S3 | [[AWS Storage Gateway]] |
| Move NFS or SMB data on a schedule | [[AWS DataSync]] |
| SFTP into S3 | [[AWS Transfer Family]] |
| Migrate a database with little downtime | [[AWS DMS]] |
| Lift and shift servers | [[AWS Application Migration Service]] |
| Decouple with a queue | [[Amazon SQS]] |
| Order and exactly-once processing | [[SQS FIFO Queues]] |
| Route events on content | [[Amazon EventBridge]] |
| Workflow with retries and human approval | [[AWS Step Functions]] |
| Replay a stream | [[Kinesis Data Streams]] |
| Load streaming data into S3 with no code | [[Amazon Data Firehose]] |
| SQL on S3 | [[Amazon Athena]] |
| Data warehouse | [[Amazon Redshift]] |
| Convert CSV to [[Data Formats\|Parquet]] | [[AWS Glue]] |
| Graph relationships | [[Amazon Neptune]] |
| Extract text from scanned documents | [[Amazon Textract]] |
| Sentiment analysis | [[Amazon Comprehend]] |

---
**Up:** [[SAA-C03 Exam Overview]]
