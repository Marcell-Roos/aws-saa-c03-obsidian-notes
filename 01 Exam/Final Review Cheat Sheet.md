---
tags: [exam, scope/in]
aliases: ["Cheat Sheet", "Keyword Cheat Sheet", "Exam Traps", "Limits and Numbers", "Must-Know Combos", "Important Ports"]
---

# Final Review Cheat Sheet

Read this in the last few days before the exam. It collects the keywords, traps and numbers from every chapter. It is not a substitute for the chapters, because the exam asks you to reason, not to recall one line.

Parts of the traps table are adapted from [RonitSachdev/aws-saa-c03-guides](https://github.com/RonitSachdev/aws-saa-c03-guides) (CC BY 4.0), with changes. See [[Licences and Attribution]].

## Keyword to service

### Compute and scaling

| Words in the question | Think |
| --- | --- |
| Short event-driven code | Lambda |
| Job longer than 15 minutes | Fargate, ECS or AWS Batch |
| Containers, no servers | Fargate |
| Existing Kubernetes | EKS |
| GPU containers | ECS or EKS on EC2 |
| Hundreds of thousands of batch jobs | AWS Batch |
| Deploy a web app quickly, keep control | Elastic Beanstalk |
| Interruptible, cheapest | Spot |
| Steady for years, fixed family | Standard RI or EC2 Instance Savings Plan |
| Steady spending, flexible, includes Fargate and Lambda | Compute Savings Plan |
| Guarantee capacity in one AZ | Capacity Reservation or zonal RI |
| Per-socket licences | Dedicated Host |
| Lowest latency between nodes | Cluster placement group, EFA |
| Isolate a few critical instances | Spread placement group |
| Kafka, Cassandra, Hadoop on EC2 | Partition placement group |
| Keep RAM across a stop | Hibernate |
| Keep a metric at a value | Target tracking |
| Known time pattern | Scheduled scaling |
| Recurring pattern, forecast | Predictive scaling |
| Workers scale on a backlog | Queue depth or backlog per instance |
| Must stay on-premises, with AWS APIs | Outposts |
| 5G devices | Wavelength |
| One metro area | Local Zones |

### Load balancing and networking

| Words in the question | Think |
| --- | --- |
| Path or host routing | ALB |
| Static IP, UDP, extreme performance | NLB |
| Static anycast IPs, TCP or UDP, global | Global Accelerator |
| Third-party firewall appliances | Gateway Load Balancer |
| Many certificates, one listener | SNI |
| Real client IP behind an ALB | `X-Forwarded-For` |
| Block one IP | Network ACL |
| Tier-to-tier access | Security group reference |
| Private subnet outbound internet | NAT gateway |
| IPv6 outbound only | Egress-only internet gateway |
| S3 or DynamoDB, private and free | Gateway endpoint |
| Other AWS services privately | Interface endpoint |
| Few VPCs, cheapest | VPC peering |
| Many VPCs and on-premises | Transit Gateway |
| One service, overlapping CIDRs | PrivateLink |
| Share subnets across accounts | AWS RAM |
| Encrypted link in hours | Site-to-Site VPN |
| Consistent bandwidth, no internet | Direct Connect |
| Direct Connect to many Regions | Direct Connect Gateway |
| Laptops to a VPC | Client VPN |
| No port 22 admin access | Session Manager |
| Accept or reject traffic data | VPC Flow Logs |
| Copy packets for inspection | Traffic Mirroring |
| Filter domains for a whole VPC | Network Firewall |

### Route 53 and edge

| Words in the question | Think |
| --- | --- |
| Zone apex to an AWS resource | Alias record |
| Active-passive | Failover routing |
| 10% canary | Weighted routing |
| Country rules, compliance | Geolocation routing |
| Best performance | Latency routing |
| Shift traffic with a bias | Geoproximity routing |
| Client IP ranges | IP-based routing |
| Private endpoint health | CloudWatch alarm health check |
| On-premises resolves AWS names | Inbound Resolver endpoint |
| AWS resolves on-premises names | Outbound Resolver endpoint |
| Cache global content | CloudFront |
| Private bucket behind CloudFront | Origin Access Control |
| One paid file | Signed URL |
| Whole paid library | Signed cookies |
| Block countries | Geo restriction |
| Certificate for CloudFront | ACM in us-east-1 |
| Headers and URL changes at scale | CloudFront Functions |
| Edge logic with network calls | Lambda@Edge |
| Global uploads to one bucket | S3 Transfer Acceleration |

### Storage

| Words in the question | Think |
| --- | --- |
| Unknown access pattern | S3 Intelligent-Tiering |
| Can be recreated, infrequent | S3 One Zone-IA |
| Archive, milliseconds | Glacier Instant Retrieval |
| Archive, 1 to 5 minutes | Glacier Flexible Retrieval, Expedited |
| Cheapest, 12 hours or more | Glacier Deep Archive |
| WORM, not even root | Object Lock, Compliance mode |
| Lawsuit, no end date | Legal hold |
| Temporary link, no AWS account | Presigned URL |
| Old objects were not replicated | S3 Batch Replication |
| Bulk changes to existing objects | S3 Batch Operations |
| Shared Linux files | EFS |
| Windows, SMB, Active Directory | FSx for Windows |
| HPC, ML, data in S3 | FSx for Lustre |
| NetApp, multi-protocol | FSx for ONTAP |
| ZFS | FSx for OpenZFS |
| Temporary, fastest | Instance store |
| Critical database IOPS | io2 Block Express |
| General database IOPS, cost-effective | gp3 |
| Large sequential reads, cheap | st1 |
| Replace tapes | Tape Gateway |
| On-premises files stored in S3 | S3 File Gateway |
| Partners use SFTP | Transfer Family |
| Migrate or sync file data | DataSync |

### Databases

| Words in the question | Think |
| --- | --- |
| Automatic failover | Multi-AZ |
| Offload reporting | Read replica |
| Same reads repeated | ElastiCache |
| Too many connections from Lambda | RDS Proxy |
| Global relational, about 1 second RPO | Aurora Global Database |
| Multi-Region writes, NoSQL | DynamoDB global tables |
| Microsecond DynamoDB reads | DAX |
| Spiky relational | Aurora Serverless v2 |
| Spiky NoSQL | DynamoDB on-demand |
| Instant copy for testing | Aurora cloning |
| Undo a mistake in place | Aurora Backtrack |
| Item changes trigger code | DynamoDB Streams and Lambda |
| Auto-expire items | DynamoDB TTL |
| Leaderboard | Valkey or Redis sorted sets |
| Graph, relationships | Neptune |
| MongoDB | DocumentDB |
| Cassandra | Keyspaces |
| Data warehouse | Redshift |
| Different database engines | DMS with SCT |

### Integration and analytics

| Words in the question | Think |
| --- | --- |
| Decouple with a queue | SQS |
| Order and exactly once | SQS FIFO |
| One event, many durable consumers | SNS to SQS fan-out |
| Route on content, SaaS events | EventBridge |
| Serverless cron | EventBridge Scheduler |
| Workflow, retries, approvals | Step Functions |
| AMQP, MQTT, JMS, RabbitMQ | Amazon MQ |
| Replay a stream, many consumers | Kinesis Data Streams |
| Load streams into S3 with no code | Data Firehose |
| Kafka | MSK |
| Video | Kinesis Video Streams |
| SQL on S3 | Athena |
| Convert CSV to Parquet | Glue |
| Hadoop or Spark | EMR |
| Query S3 from Redshift | Redshift Spectrum |
| Row and column security on a data lake | Lake Formation |
| Fuzzy search | OpenSearch |
| BI dashboards | Amazon Quick |
| SaaS data to S3 | AppFlow |

### Security and operations

| Words in the question | Think |
| --- | --- |
| Temporary credentials | STS |
| Workforce single sign-on | IAM Identity Center |
| App users sign-in | Cognito user pool |
| App users need AWS credentials | Cognito identity pool |
| Org-wide ceiling | SCP |
| Stop outsiders reaching resources | RCP |
| Ceiling for one identity | Permission boundary |
| Best-practice multi-account setup | Control Tower |
| Audit key use | SSE-KMS |
| Single-tenant HSM | CloudHSM |
| Same key across Regions | KMS Multi-Region keys |
| Rotate database credentials | Secrets Manager |
| Cheap config store | Parameter Store |
| SQL injection, rate limits | WAF |
| DDoS | Shield |
| Rules across an organisation | Firewall Manager |
| Threats from logs | GuardDuty |
| Software vulnerabilities | Inspector |
| PII in S3 | Macie |
| Root cause of a finding | Detective |
| One view of findings | Security Hub |
| AWS's compliance reports | Artifact |
| Who did it? | CloudTrail |
| What changed, is it compliant? | AWS Config |
| How is it performing? | CloudWatch |
| Which microservice is slow? | X-Ray |
| Preview a template change | CloudFormation change sets |
| Many accounts and Regions | StackSets |
| Scan and rightsize | Compute Optimizer |
| Alert at a spending level | AWS Budgets |
| Line-item bills with SQL | CUR and Athena |

### Migration and recovery

| Words in the question | Think |
| --- | --- |
| Lift and shift servers | Application Migration Service |
| Migrate a database with little downtime | DMS with CDC |
| Data would take over a week | Snow Family or Data Transfer Terminal |
| Cheapest DR, hours acceptable | Backup and restore |
| Data live, servers off | Pilot light |
| Small running copy | Warm standby |
| Zero downtime across Regions | Multi-site active-active |
| Central backups | AWS Backup |
| Undeletable backups | Backup Vault Lock, compliance mode |

### Machine learning

| Words in the question | Think |
| --- | --- |
| Faces and objects in images | Rekognition |
| Forms and tables in documents | Textract |
| Speech to text | Transcribe |
| Text to speech | Polly |
| Translation | Translate |
| Sentiment | Comprehend |
| Chatbot | Lex |
| Custom model | SageMaker AI |

## Traps

| Trap | Truth |
| --- | --- |
| Read from the Multi-AZ standby | An instance standby is not readable. A Multi-AZ DB cluster has two readable standbys |
| Replicas fail over automatically | Promotion is manual |
| CNAME at the zone apex | Not allowed. Use an Alias |
| Add a deny rule to a security group | Security groups only allow. Deny lives in NACLs |
| Security groups need return rules | They are stateful. NACLs need ephemeral port rules |
| Reach S3 through NAT | Works, but costs money. A gateway endpoint is free |
| Gateway endpoints from on-premises | Not reachable. Use an interface endpoint |
| Run a 20-minute job in Lambda | Lambda stops at 15 minutes |
| Mount EFS on Windows | EFS is Linux only. Use FSx for Windows |
| Snowball imports directly into Glacier | It lands in S3, then a lifecycle rule moves it |
| A-B and B-C peering lets A reach C | Peering is not transitive |
| Peer overlapping CIDRs | Not allowed. PrivateLink works |
| Encrypt an existing RDS or EBS volume in place | Impossible. Snapshot, copy with encryption, restore |
| FIPS Level 3 means CloudHSM | KMS HSMs are FIPS 140-3 Level 3 too. The difference is single tenancy. Older questions may still expect CloudHSM |
| Shield Standard stops layer 7 attacks | Standard covers layers 3 and 4. Layer 7 needs WAF or Shield Advanced |
| WAF on an NLB | Not supported |
| Apply an SCP to the management account | SCPs never affect it |
| SCPs grant permissions | They are ceilings only |
| Config prevents changes | Config detects. SCPs and IAM prevent |
| Replay DynamoDB Streams from last month | Streams keep 24 hours |
| Give an ALB a static IP | ALBs have none. Use an NLB or Global Accelerator |
| Add an LSI to an existing table | LSIs are set at creation. Add a GSI |
| Strong reads on a GSI | GSIs are eventually consistent |
| Accelerate UDP with CloudFront | Use Global Accelerator |
| CloudFront for global uploads | Use Transfer Acceleration |
| Parameter Store rotates passwords | No native rotation. Use Secrets Manager |
| One NAT gateway serves all AZs | A zonal gateway dies with its AZ |
| SNS keeps messages for offline consumers | It does not persist them. Use SNS to SQS |
| Firehose offers replay | It does not store data. Use Kinesis Data Streams |
| Direct Connect is encrypted | It is private, not encrypted. Add VPN or MACsec |
| Spot for a critical database | Never. It can be reclaimed |
| Savings Plans reserve capacity | They do not. Capacity Reservations and zonal RIs do |
| Delete a KMS key immediately | 7 to 30 day wait. Disable it instead |
| ACM renews imported certificates | It does not |
| ACM certificate for CloudFront in your own Region | It must be in us-east-1 |
| Lifecycle transitions upwards | Waterfall only goes down |
| S3 replicates existing objects | Only new ones. Use Batch Replication |
| S3 events to a FIFO queue | Not supported directly |
| Data deleted from S3 Standard-IA after 10 days | Billed for 30 |
| Automated RDS backups for 7 years | Maximum is 35 days |
| Beanstalk-created RDS survives | It is deleted with the environment |
| Fargate with GPUs | Not supported |
| Memory metric by default | Needs the CloudWatch agent |
| Session Manager needs port 22 | It needs no inbound ports |
| Max I/O for EFS scale | Previous generation. Use General Purpose |

## Numbers

### Compute

| Item | Value |
| --- | --- |
| Lambda memory | 128 MB to 10,240 MB |
| Lambda timeout | 15 minutes |
| Lambda `/tmp` | 512 MB to 10,240 MB |
| Lambda package | 50 MB zipped, 250 MB unzipped, 10 GB image |
| Lambda payload | 6 MB sync, 1 MB async, 200 MB streamed |
| Lambda environment variables, layers | 4 KB, 5 layers |
| Lambda concurrency | 1,000 by default, +1,000 environments per 10 seconds per function |
| RI discount | Standard up to 72%, Convertible up to 66% |
| Savings Plans discount | EC2 Instance up to 72%, Compute up to 66%, SageMaker AI up to 64%, Database up to 35% on a 1-year term |
| Spot | Up to 90% off, 2-minute notice |
| Spread placement | 7 running instances per AZ |
| Partition placement | 7 partitions per AZ |
| Hibernate RAM | Under 150 GiB on Linux, 16 GiB or less on Windows |
| ASG default cooldown | 300 seconds |
| ELB deregistration delay | 300 seconds by default, 1 to 3,600 |
| Fargate ephemeral storage | 20 GiB default, up to 200 GiB |

### Storage

| Item | Value |
| --- | --- |
| S3 maximum object | 48.8 TiB, usually rounded to 50 TB. Older questions say 5 TB |
| S3 multipart | Recommended over 100 MB, required over 5 GiB, 10,000 parts |
| S3 requests per prefix | 3,500 writes, 5,500 reads per second |
| S3 durability | 11 nines |
| Presigned URL | 12 hours in console, 7 days with the CLI |
| Minimum storage duration | IA 30, Glacier Instant 90, Flexible 90, Deep Archive 180 days |
| Glacier Flexible retrieval | 1 to 5 minutes, 3 to 5 hours, 5 to 12 hours |
| Deep Archive retrieval | 12 hours, 48 hours |
| gp3 | 1 GiB to 64 TiB, 3,000 to 80,000 IOPS, 125 to 2,000 MiB/s |
| gp2 | Up to 16 TiB, 16,000 IOPS, 3 IOPS per GiB |
| io2 Block Express | 64 TiB, 256,000 IOPS, 4,000 MiB/s, 99.999% durability |
| st1, sc1 | 500 MiB/s, 250 MiB/s. Neither can boot |
| Multi-Attach | io1 or io2, 16 Nitro instances in one AZ |

### Databases

| Item | Value |
| --- | --- |
| RDS read replicas | 15, with no more than 5 recommended for Oracle |
| RDS backup retention | 0 to 35 days |
| Multi-AZ instance failover | Typically 1 to 2 minutes |
| Aurora | 6 copies in 3 AZs, 15 replicas, 256 TiB, failover under 30 seconds |
| Aurora Global Database | 10 secondary Regions, 16 replicas each |
| Aurora Backtrack | Up to 72 hours |
| DynamoDB item | 400 KB |
| DynamoDB RCU | 1 strong or 2 eventual reads per second, up to 4 KB |
| DynamoDB WCU | 1 write per second, up to 1 KB |
| DynamoDB PITR | 35 days |
| DynamoDB Streams | 24 hours |
| DynamoDB indexes | 20 GSIs, 5 LSIs |
| DAX default TTL | 5 minutes |

### Networking

| Item | Value |
| --- | --- |
| VPC CIDR | /16 to /28 |
| Reserved IPs per subnet | 5 |
| VPCs per Region | 5 |
| Security groups per interface | 5 |
| Security group rules | 60 inbound, 60 outbound |
| NACL rules | 20 per direction, up to 40 |
| Ephemeral ports | 1024 to 65535 |
| VPN tunnel | 1.25 Gbps, 5 Gbps with a large bandwidth tunnel |
| Direct Connect, dedicated | 1, 10, 100, 400 Gbps |
| Direct Connect, hosted | 50 Mbps to 25 Gbps |
| Transit Gateway | 5,000 attachments, up to 100 Gbps per VPC attachment per AZ |
| Route 53 multivalue | 8 healthy records |
| API Gateway timeout | 29 seconds by default |
| API Gateway payload | 10 MB |
| API Gateway throttle | 10,000 requests per second |
| API Gateway cache | 300 seconds by default |

### Messaging and streaming

| Item | Value |
| --- | --- |
| SQS message | 1 MiB |
| SQS retention | 1 minute to 14 days, default 4 days |
| SQS visibility timeout | Default 30 seconds, up to 12 hours |
| SQS delay | Up to 15 minutes |
| SQS long polling | Up to 20 seconds |
| SQS FIFO | 300 per second, 3,000 with batching, up to 70,000 in high-throughput mode |
| SNS message | 256 KiB default, up to 1 MiB |
| Kinesis retention | 24 hours to 365 days |
| Kinesis shard | 1 MB/s or 1,000 records per second in, 2 MB/s out |
| Step Functions | Standard 1 year, Express 5 minutes |

### Security and monitoring

| Item | Value |
| --- | --- |
| IAM role session | 1 hour by default, up to 12 hours |
| KMS direct encryption | 4 KB |
| KMS key deletion wait | 7 to 30 days |
| KMS rotation | Yearly by default, custom 90 to 2,560 days |
| Secrets Manager secret | 64 KB |
| Parameter Store | 4 KB standard, 8 KB advanced |
| ACM expiry events | Start 45 days before |
| Shield Advanced | $3,000 per month per organisation |
| CloudTrail event history | 90 days |
| EC2 metrics | 5 minutes, or 1 minute with detailed monitoring |
| Budgets refresh | Up to three times a day |

### Ports

SSH and SFTP 22, DNS 53, HTTP 80, HTTPS 443, SMB 445, SQL Server 1433, Oracle 1521, NFS 2049, MySQL and MariaDB 3306, RDP 3389, PostgreSQL 5432, Redis and Valkey 6379, GENEVE 6081, Memcached 11211.

## Combinations to remember

| Need | Combination |
| --- | --- |
| Serverless web app | CloudFront, S3, API Gateway, Lambda, DynamoDB |
| Reliable fan-out | SNS to multiple SQS queues |
| Global database | Aurora Global Database, or DynamoDB global tables |
| Protect a web app | CloudFront, WAF, Shield, ALB |
| Real-time pipeline | Kinesis Data Streams, Lambda, DynamoDB or S3 |
| Data lake analytics | S3, Glue, Athena, Amazon Quick |
| Migration toolkit | DataSync, DMS, Direct Connect |
| DR stack | Route 53 failover, Aurora Global Database, S3 CRR |
| App sign-in | Cognito user pools and identity pools |

---
**Previous:** [[Exam Technique]] · **Plan:** [[Study Guide]]
