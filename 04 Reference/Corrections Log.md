---
tags: [reference, scope/in]
---

# Corrections Log

This page records how the vault's facts were checked, and what changed. The newest work comes first.

## Review on 2 November 2026

The whole vault was read line by line: 31 chapters, 5 practice exams (325 questions), 272 self-test questions, the labs and the reference pages. This was a review by Claude, the AI that wrote the vault, and not an independent human review.

**Scripted checks, all passed:** all 189 exam guide items match AWS's text word for word, all 119 in-scope and 50 out-of-scope entries match, every internal link resolves, and all 5 answer keys and domain tables match their questions.

**Checked against live AWS pages:** the claims listed below, the lifecycle dates, the exam facts and policies, and the items previously marked as not confirmed. Other facts were checked by the reviewer's own knowledge, not against a page.

### Errors corrected

| Note said | Now | Why |
| --- | --- | --- |
| FSx for Windows can use AD Connector, including the answer to chapter 2 question 9 | FSx joins AWS Managed Microsoft AD or a self-managed AD directly. Question 9 rewritten | [AWS](https://docs.aws.amazon.com/fsx/latest/WindowsGuide/aws-ad-integration-fsxW.html) gives only these two options |
| EventBridge reaches S3 through a resource-based policy | CloudWatch Logs in that list, not S3 | [AWS](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-use-resource-based.html) |
| Practice Exam 4 question 34 offered Glacier Instant Retrieval against One Zone-IA | Option replaced with Standard-IA | The old answer was ambiguous, and it conflicted with the flow chart in chapter 6 |
| Use the Storage Gateway hardware appliance without virtualisation | No longer offered | [AWS](https://docs.aws.amazon.com/filegateway/latest/files3/hardware-appliance.html) |
| DynamoDB TTL deletes within about 48 hours | Typically within a few days | [AWS](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/TTL.html) |
| IPv6 in a VPC has no private range | AWS offers public and private IPv6 addresses | [AWS](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-ip-addressing.html) |
| Cost Explorer forecasts 12 months | 18 months | [AWS](https://docs.aws.amazon.com/cost-management/latest/userguide/ce-what-is.html) |
| Compute Optimizer covers compute only | Also Aurora, RDS, DynamoDB, NAT gateways and licences | [AWS](https://docs.aws.amazon.com/compute-optimizer/latest/ug/what-is-compute-optimizer.html) |
| Interface endpoints cover most services and S3 | DynamoDB too | [AWS](https://docs.aws.amazon.com/vpc/latest/privatelink/aws-services-privatelink-support.html) |
| Savings Plans are always 1 or 3 years | Database Savings Plans are 1 year | [AWS](https://aws.amazon.com/savingsplans/database-pricing/) |
| Recycle Bin covers snapshots and AMIs | EBS volumes too | [AWS](https://docs.aws.amazon.com/ebs/latest/userguide/recycle-bin.html) |
| Nitro is needed for enhanced networking | Removed | Enhanced networking is not limited to Nitro instances |
| Lab 8: a message reaches the DLQ after two receives | It moves on the next attempt, when the count passes `maxReceiveCount` | [AWS](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-dead-letter-queues.html) |

### Gaps filled

S3 Express One Zone's minimum storage, shown as None in [AWS's table](https://docs.aws.amazon.com/AmazonS3/latest/userguide/storage-class-intro.html). EventBridge's event size. Centralised root access, ECS Service Connect, ECS EBS volumes, reserved capacity for databases, Amazon Quick row-level security, FSx data deduplication, EFS encryption being set at creation, MRSC needing three Regions, and the features listed as in maintenance for Comprehend, Rekognition, ARC and SNS. Role chaining's one-hour limit.

### Suspected, then cleared

These looked wrong, and were confirmed as correct: precision time placement groups, QUIC on NLB, the Database Savings Plan service list, RDS Storage Auto Scaling conditions, 80,000 IOPS on gp3, regional NAT gateway limits, Lambda Web Functions, the newer EventBridge custom event bus, and combined cross-Region and cross-account copies for RDS in AWS Backup.

## November 2026 rewrite

The vault was rebuilt on 1 November 2026. The 490 short notes were consolidated into 31 study chapters, with a study guide, 11 labs, five practice exams and a Service Index added. All notes were rewritten, which also removed the spelling and grammar errors in the source text.

**How it was checked:** AWS's exam guide pages were read in full, and more than 100 official AWS pages were read to check specific claims. All 14 task statements, all 119 in-scope services and the out-of-scope list were compared with AWS's pages.

### Errors and outdated facts found

| Earlier note said | Now | Why |
| --- | --- | --- |
| Global tables need DynamoDB Streams | No setup is needed | A leftover in the old drill. AWS handles replication |
| EFS Max I/O suits thousands of clients | Use General Purpose. Max I/O is a previous-generation mode | [AWS](https://docs.aws.amazon.com/efs/latest/ug/performance.html) |
| Snapshot Archive restores in 24 to 72 hours | Up to 72 hours | [AWS](https://docs.aws.amazon.com/ebs/latest/userguide/snapshot-archive.html) |
| EFS Replication goes to another Region or AZ | To another Region | [AWS](https://docs.aws.amazon.com/efs/latest/ug/efs-replication.html) |
| The 29-second API Gateway timeout cannot be raised | 29 seconds is the default, and can be raised for Regional and private APIs | The old drill contradicted the service note |
| RDS Storage Auto Scaling waits 6 hours | Needs storage optimisation finished, and fewer than four changes in 24 hours | [AWS](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_PIOPS.Autoscaling.html) |
| Aurora Global Database RTO under 1 minute | Docs say a few minutes for failover, and under 30 seconds for switchover on recent versions. Older figures noted | [AWS](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/aurora-global-database-disaster-recovery.html) |
| Spot is lost when your maximum price is passed | AWS reclaims it when it needs the capacity | Current Spot behaviour |
| SR-IOV is an alternative to ENA | SR-IOV is the mechanism behind enhanced networking | The old note was misleading |
| IAM Access Analyzer covers S3 | It covers many resource types, and unused access | The old note was too narrow |
| ONTAP supports NFS, SMB and iSCSI | Also NVMe | [AWS](https://docs.aws.amazon.com/fsx/latest/ONTAPGuide/what-is-fsx-ontap.html) |

### New facts added

Regional NAT gateway details, Transit Gateway 100 Gbps per attachment per AZ, Direct Connect LAG limits, 500 routes per route table, Database Savings Plans, Fargate storage up to 200 GiB, CloudFront flat-rate plans, the fourth Route 53 health check type, certification retake and ID rules, ESL +30, and precision time placement groups.

### Not confirmed on a page read

The review on 2 November 2026 confirmed all but one of the items first listed here, and the rest are now removed. The one left is the usual 30-day wait before a lifecycle transition to Standard-IA, because current docs describe it through storage charges.

**Conflicts in AWS's own pages:** the Lambda@Edge viewer timeout appears as 30 seconds in the current comparison table, where older material says 5 seconds. EFS One Zone availability appears with two different figures.

## Earlier work

The rest of this page is the log from the vault's first version.

Every change made to the source notes (VasilijeJukic01/AWS-SAA-C03-Notes), checked against AWS documentation on 1 November 2026. Spelling fixes aren't itemised.

## Factual errors fixed

| Original | Now | Why |
| --- | --- | --- |
| RDS Proxy enforces IAM authentication for the database and securely stores credentials in SSM. | RDS Proxy can enforce IAM authentication for clients and reads database credentials from AWS Secrets Manager. | Credentials live in Secrets Manager, not SSM, and IAM auth is optional. [AWS](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/rds-proxy.html) |
| recommended for files < 100MB, must use for files >5GB | recommended for files over 100 MB, required for objects over 5 GiB | The threshold was reversed. [AWS](https://docs.aws.amazon.com/AmazonS3/latest/userguide/mpuoverview.html) |
| Once data is inserted in Kinesis, it cant be deleted. | Records are immutable: they can't be deleted individually and expire when the retention period ends (24 hours by default, up to 365 days). | Misleading: records do expire. [AWS](https://docs.aws.amazon.com/streams/latest/dev/service-sizes-and-limits.html) |
| Automate backups up to 36 days with PITR | Automate backups up to 35 days with PITR | PITR is 35 days. The source contradicted itself. [AWS](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Point-in-time-recovery.html) |
| In comparison with Athena, Redshift has faster queries, joins and aggregations because it uses indexes. | Compared with Athena, Redshift is faster for complex queries, joins and aggregations because data is loaded into columnar storage and org... | Redshift doesn't use indexes. |
| -1≤ Bias ≤ -99 | -99 ≤ Bias ≤ -1 | Range was written backwards. [AWS](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-policy-geoproximity.html) |
| **X-Forwarder-For** | **X-Forwarded-For** | Header name typo, and it matters on the exam. |
| **A, AAA, CNAME, NS** | **A, AAAA, CNAME, NS** | Record type typo. |
| Network Load balancer doesn't have Weighted Target Groups. | A listener can forward to multiple target groups using weights from 0 to 999. | NLB listeners now support weighted target groups. [AWS](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/load-balancer-listeners.html) |
| Once we have created a launch template, it can't be modified. | A launch template version can't be edited, but we can create a new version and point the ASG at it. | Templates are versioned. |
| It supports all S3 classes except S3 Glacier. Transition to S3 Glacier must be done using a Lifecycle Policy. | It supports S3 Standard, Standard-IA, One Zone-IA, Intelligent-Tiering and Glacier storage classes, but not Glacier Instant Retrieval. Mo... | The source's class list was wrong. [AWS](https://docs.aws.amazon.com/filegateway/latest/files3/storage-classes.html) |
| SCP must have an explicit allow (does not allow anything by defult). | SCPs never grant permissions; they only set the maximum available. The default `FullAWSAccess` SCP allows everything, and removing it wit... | Misleading: SCPs are filters and FullAWSAccess is attached by default. [AWS](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps.html) |
| custom config rules (**must be defined in AWS Lambda**) | custom config rules (written as **Lambda functions** or as **Guard** custom policy rules) | Guard rules need no Lambda. [AWS](https://docs.aws.amazon.com/config/latest/developerguide/evaluate-config_develop-rules.html) |
| **IAM Certificate Store** is a system or service used to manage and organize digital certificates within an... | The **IAM certificate store** holds server certificates in IAM for Regions where ACM isn't available. Prefer ACM where possible: IAM can'... | The source's definition was meaningless. |
| Each role can use different ECS services. | Each role can access different AWS services. | Wrong service scope. |
| Turning on AOF ensures **local** data persistence but may not help with **regional** failures. To provide r... | AOF only protects against node restarts, not hardware or AZ failure, and in ElastiCache for Redis OSS it is mutually exclusive with Multi... | AOF and Multi-AZ are mutually exclusive; the issue is AZ, not Region. [AWS](https://docs.aws.amazon.com/AmazonElastiCache/latest/dg/AutoFailover.html) |
| we can use DynamoDB Global Databases. | we can use DynamoDB Global Tables. | No such feature as Global Databases. |
| **Import to S3** | **Import from S3** | Wrong direction. |

## Outdated facts updated

| Original | Now | Why |
| --- | --- | --- |
| Max object size is 5TB, if we upload more than 5GB, must use “multi-part upload”. | Max object size is 48.8 TiB (raised from the long-standing 5 TB limit), and anything over 5 GiB must use multipart upload. | S3 raised the maximum object size. [AWS](https://docs.aws.amazon.com/AmazonS3/latest/userguide/qfacts.html) |
| **Provisioned Mode** (default) | **Provisioned Mode** | On-demand is now the default. [AWS](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/capacity-mode.html) |
| **On-demand Mode** - read/writes automatically scale | **On-demand Mode** (default and recommended for most workloads) - read/writes automatically scale | On-demand is now the default. [AWS](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/capacity-mode.html) |
| We pay for what we use (more expensive). | We pay per request, with no idle capacity to pay for. | Reflects current AWS guidance. [AWS](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/capacity-mode.html) |
| We must enable DynamoDB Streams as a pre-requisite. | DynamoDB handles replication for us. There are two consistency modes: multi-Region eventual consistency (MREC, the default) and multi-Reg... | Global tables now offer MRSC and no manual Streams setup. [AWS](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/GlobalTables.html) |
| We must provision the node size in advance and use RI for cost savings. | On a provisioned cluster we choose the node size in advance and can use Reserved Instances for savings. Redshift Serverless removes that ... | Redshift Serverless exists. [AWS](https://docs.aws.amazon.com/redshift/latest/mgmt/serverless-whatis.html) |
| We must use Route 53 Traffic Flow to use this feature. | We can set it on records directly or build it with Route 53 Traffic Flow. | Traffic Flow is no longer the only route. [AWS](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/routing-policy-geoproximity.html) |
| The main account is called master account. | The main account is called the management account. | Renamed by AWS. |
| (does not apply to the master account) | (does not apply to the management account) | Renamed by AWS. |
| **AWS IAM Identity Center** **(AWS Single Sign-On (AWS SSO))** | **AWS IAM Identity Center** (formerly AWS SSO) | Renamed in 2022. |
| Possibility of rotation policy (new key generated every year). | Optional automatic rotation (every 365 days by default, with a custom period available) plus on-demand rotation. | KMS rotation is now configurable. [AWS](https://docs.aws.amazon.com/kms/latest/developerguide/rotate-keys.html) |
| **Automatic key rotation** is automatic every 1 year for AWS managed keys. For created CMKs it must be enab... | AWS managed keys rotate automatically every year. For customer managed keys rotation is optional (automatic or on-demand). Keys with impo... | Imported keys can now use on-demand rotation. [AWS](https://docs.aws.amazon.com/kms/latest/developerguide/importing-keys.html) |
| MSK creates and manages Kafka brokers nodes and Zookeeper nodes for us. | MSK creates and manages Kafka broker nodes and the metadata layer for us (KRaft controllers on newer clusters, ZooKeeper nodes on older o... | KRaft is supported from Kafka 3.7. [AWS](https://docs.aws.amazon.com/msk/latest/developerguide/metadata-management.html) |
| Locked to a specific instance family & AWS Region, but flexible across instance size, OS and tenancy. | **EC2 Instance Savings Plans** (up to 72% off) are locked to an instance family and Region, but flexible across size, OS and tenancy. **C... | The source described only one of the plan types. [AWS](https://docs.aws.amazon.com/savingsplans/latest/userguide/plan-types.html) |
| up to 128TB. | up to 256 TiB on recent engine versions (128 TiB on older ones). | Limit raised. [AWS](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/CHAP_Limits.html) |
| There is 1 primary region for read and write and up to 5 secondary regions for read-only. | There is 1 primary region for read and write and up to 10 secondary regions for read-only. | Limit raised from 5 to 10. [AWS](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/aurora-global-database.html) |
| **RDS Performance Insights** is a feature that helps us monitor and analyze the performance of our RDS data... | **CloudWatch Database Insights** replaced RDS Performance Insights, which reached end of life on 31 July 2026. It gives a higher-level vi... | Performance Insights was retired. [AWS](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/Database-Insights.html) |
| Oracle, Microsoft SQL Server, Aurora). | Oracle, Microsoft SQL Server, IBM Db2, Aurora). | Db2 was missing. |
| IAM database authentication works with MySQL and PostgreSQL. | IAM database authentication works with MariaDB, MySQL and PostgreSQL. | MariaDB was missing. [AWS](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/UsingWithRDS.IAMDBAuth.html) |
| ElastiCache supports two popular in-memory caching engines: | ElastiCache supports three in-memory engines: **Valkey** (the open-source Redis fork), plus the two below. It can run as a serverless cac... | Valkey and Serverless were missing. [AWS](https://docs.aws.amazon.com/AmazonElastiCache/latest/dg/WhatIs.html) |
| By default, an S3 object is owned by the AWS account that uploaded it even though the bucket is owned by an... | New buckets default to the **Bucket owner enforced** Object Ownership setting: ACLs are disabled and the bucket owner owns every object. ... | ACLs have been off by default since 2023. [AWS](https://docs.aws.amazon.com/AmazonS3/latest/userguide/about-object-ownership.html) |
| **SSE with Customer-Provided Keys (SSE-C)** - when we want to manage our own encryption keys. | **SSE with Customer-Provided Keys (SSE-C)** - when we want to manage our own encryption keys. Since April 2026 it is blocked by default o... | New default bucket setting. [AWS](https://docs.aws.amazon.com/AmazonS3/latest/userguide/ServerSideEncryptionCustomerKeys.html) |
| -   RTMP distribution (signed cookies aren't supported for RTMP distributions). | (removed) | CloudFront RTMP distributions were discontinued. |
| The minimum expiration time CloudFront supports is 0 seconds for web distributions and 3600 seconds for RTM... | The minimum expiration time CloudFront supports is 0 seconds. | RTMP was discontinued. |
| **Origin Access Identity (OAI)** is a special CloudFront user that we can create to give CloudFront permiss... | **Origin Access Identity (OAI)** is the legacy way to give CloudFront access to an S3 bucket. AWS recommends OAC instead. | OAI is legacy. [AWS](https://docs.aws.amazon.com/AmazonCloudFront/latest/DeveloperGuide/private-content-restricting-access-to-s3.html) |
| improves our Lambda functions performance up to 10x at **no extra cost** for Java 11 and above. | improves startup performance by up to 10x. It supports Java 11+ (no extra cost) plus Python 3.12+ and .NET 8+ (which are charged for snap... | More runtimes are supported, and only Java is free. [AWS](https://docs.aws.amazon.com/lambda/latest/dg/snapstart.html) |
| **Control Tower Guardrails** | **Control Tower Controls** (formerly guardrails) | Renamed by AWS. [AWS](https://docs.aws.amazon.com/controltower/latest/controlreference/controls.html) |
| Automate ongoing policy management using guardrails. | Automate ongoing policy management using controls. | Renamed by AWS. |
| **Preventive Guardrail** | **Preventive control** | Renamed by AWS. |
| **Detective Guardrail** | **Detective control** | Renamed by AWS. |
| -   **Amazon Linux 2 AMI as VM** (.iso format) | -   **Amazon Linux VM images** - run Amazon Linux on-premises. AL2023 ships KVM (qcow2), VMware (OVA) and Hyper-V (vhdx) images. | AL2023 uses these formats. [AWS](https://docs.aws.amazon.com/linux/al2023/ug/outside-ec2.html) |
| **Glue Elastic Views** - combine and replicate data across multiple data stores using SQL. No custom code i... | (removed) | Glue Elastic Views doesn't appear in current Glue docs. [AWS](https://docs.aws.amazon.com/glue/latest/dg/what-is-glue.html) |
| **Master Node** | **Primary Node** (formerly master) | Renamed by AWS. |
| **QuickSight** is a serverless | **Amazon Quick Sight** (now part of **Amazon Quick**, formerly Amazon QuickSight) is a serverless | Renamed: the exam guide says Amazon Quick. [AWS](https://docs.aws.amazon.com/quick/latest/userguide/what-is.html) |
| 1Gpbs, 10 Gbps, 100 Gbps capacity | 1, 10, 100 and 400 Gbps capacity | 400 Gbps added. [AWS](https://docs.aws.amazon.com/directconnect/latest/UserGuide/dedicated_connection.html) |
| 50Mbps, 500 Mbps, to 10 Gbps. | 50 Mbps up to 25 Gbps. | Range widened. [AWS](https://docs.aws.amazon.com/directconnect/latest/UserGuide/hosted_connection.html) |
| NAT Gateway is created in a specific AZ and uses an Elastic IP. | A classic (zonal) NAT Gateway is created in a specific AZ and uses an Elastic IP. A **regional NAT Gateway** spans AZs automatically and ... | Regional NAT Gateways now exist. [AWS](https://docs.aws.amazon.com/vpc/latest/userguide/nat-gateways-regional.html) |
| NAT Gateway is resilient within a single AZ. | A zonal NAT Gateway is resilient within a single AZ. | Regional NAT Gateways now exist. [AWS](https://docs.aws.amazon.com/vpc/latest/userguide/nat-gateways-regional.html) |
| For Business & Enterprise Support plan: | For Business Support+, Enterprise Support and Unified Operations plans: | Support plans changed. [AWS](https://docs.aws.amazon.com/awssupport/latest/user/trusted-advisor.html) |
| **Max I/O** - ideal for applications requiring high levels of aggregate throughput and parallelism, such as... | **Max I/O** - historically for highly parallel workloads, but it has higher latency and AWS now recommends always using General Purpose. | Current AWS guidance. [AWS](https://docs.aws.amazon.com/efs/latest/ug/performance.html) |
| -   U2F (Universal 2nd Factor) (YubiKey)      Support for multiple root and IAM users using a single securi... | -   Passkeys and FIDO security keys (YubiKey)      Support for multiple root and IAM users using a single security key. | AWS now uses passkey and FIDO terminology. [AWS](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_mfa.html) |

## Service lifecycle changes

| Original | Now | Why |
| --- | --- | --- |
| **S3 Glacier Vault Lock** lets us adopt | **S3 Glacier Vault Lock** (for legacy Glacier vaults) lets us adopt | Direct vault access is in maintenance. [AWS](https://docs.aws.amazon.com/general/latest/gr/maintenance_services.html) |
| **Step Functions Local** is a tool that allows us to run and test our Step Functions state machines locally... | **Step Functions Local** let us test state machines on a development machine, but AWS now marks it as unsupported. | Now unsupported. [AWS](https://docs.aws.amazon.com/step-functions/latest/dg/sfn-local.html) |
| **FSx File Gateway** - offers native access | **FSx File Gateway** (no longer available to new customers) - offers native access | In maintenance since October 2024. [AWS](https://docs.aws.amazon.com/general/latest/gr/maintenance_services.html) |
| -   **AWS Server Migration Service** - incremental replication of on-premise live servers to AWS. | -   **AWS Application Migration Service (MGN)** - replicates live servers to AWS. It replaced the Server Migration Service, which shut do... | SMS was shut down. [AWS](https://docs.aws.amazon.com/general/latest/gr/full_shutdown_services.html) |
| **Agentless Discovery** (**AWS Agentless Discovery Connector**) | **Agentless Discovery** (**AWS Agentless Collector**; the older Discovery Connector shut down on 17 November 2025) | Discovery Connector was shut down. [AWS](https://docs.aws.amazon.com/general/latest/gr/full_shutdown_services.html) |
| **Application Composer** - A visual tool | **AWS Infrastructure Composer** (formerly Application Composer; end of support 29 September 2027) - A visual tool | Renamed and in sunset. [AWS](https://docs.aws.amazon.com/general/latest/gr/sunset_services.html) |

## Clarified or qualified

| Original | Now | Why |
| --- | --- | --- |
| Redshift loads data once every hour, not every second and it has 10x better performance than other data war... | Data is loaded in batches rather than row by row. AWS quotes up to 10x better performance than other data warehouses, and it scales to PB... | Removed the arbitrary 'once every hour' claim; marked the vendor figure. |
| It supports IP Multicast (**not supported by any other AWS service**). | It is the service to use for IP multicast between VPC subnets. | Overstated claim. [AWS](https://docs.aws.amazon.com/vpc/latest/tgw/tgw-multicast-overview.html) |
| TLS Certificate must be in the same region as CloudFront. | the TLS certificate must be in us-east-1 (CloudFront's certificate Region). | Vague: the Region is us-east-1. |
| We could use sticky session to save shoping cart but it will violate EC2 performance. | We could use sticky sessions to keep the shopping cart, but that makes instances stateful and can unbalance the load. | The original reasoning was unclear. |
| ($3000 per month) | ($3,000 per month per organization, plus data transfer fees) | Added the pricing scope. Check the current price page. [AWS](https://aws.amazon.com/shield/pricing/) |
| Only gp2/gp3 and io1/io2 Block Express can be used as boot volumes. | Only SSD volumes (gp2, gp3, io1, io2 Block Express) can be boot volumes. st1 and sc1 can't. | Clarified. [AWS](https://docs.aws.amazon.com/ebs/latest/userguide/ebs-volume-types.html) |
| we are in the cooldown period (default 300s). | we are in the cooldown period (default 300s, and it only applies to simple scaling policies). | AWS recommends target tracking or step scaling over simple scaling. [AWS](https://docs.aws.amazon.com/autoscaling/ec2/userguide/ec2-auto-scaling-scaling-cooldowns.html) |
| **ALB**: Cross-Zone Load Balancing is enabled by default and can be disabled at the target group level. | **ALB**: Cross-Zone Load Balancing is always enabled at the load balancer level and can be turned off at the target group level. | Precise behaviour. [AWS](https://docs.aws.amazon.com/elasticloadbalancing/latest/userguide/how-elastic-load-balancing-works.html) |
| **NLB**: It is disabled by default | **NLB** and **GWLB**: It is disabled by default | GWLB behaves the same way. [AWS](https://docs.aws.amazon.com/elasticloadbalancing/latest/userguide/how-elastic-load-balancing-works.html) |
| It is zero downtime operation. | No downtime is needed, although latency can rise while the standby syncs. | A performance impact is expected. |
| Aurora has 3x performance improvement over Postgres and 5x performance improvement over MySQL. | AWS quotes up to 3x the throughput of PostgreSQL and up to 5x that of MySQL. | Vendor figure, stated as 'up to'. |
| We can have up to 15 Aurora read replicas for reads and they all support CRR. | We can have up to 15 Aurora read replicas. | Removed the confusing CRR claim. |
| (max 15) | (max 15; AWS recommends no more than 5 for Oracle) | Added the Oracle caveat. [AWS](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/CHAP_Limits.html) |
| We pay $0.50 per month per hosted zone. | We pay $0.50 per month per hosted zone (for the first 25 zones). | Added the pricing tier. [AWS](https://aws.amazon.com/route53/pricing/) |
| Has 99,9% availability. | Has 99.9% availability. | Decimal format. |
| (60% improvement) | (AWS quotes up to 60%) | Vendor figure. |
| It is enabled by default. We can get history | Event history is on by default for every account and keeps 90 days of management events; to keep events longer we create a **trail**. We ... | Event history and trails are different things. [AWS](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/view-cloudtrail-events.html) |
| Even root user cannot delete backups when enabled. | In **compliance mode** not even the root user can delete backups once the grace period ends. In **governance mode**, users with sufficien... | Only true of compliance mode. [AWS](https://docs.aws.amazon.com/aws-backup/latest/devguide/vault-lock.html) |
| We cant use it on-premises. | (removed) | Removed: claim couldn't be confirmed in the docs. [AWS](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/ContainerInsights.html) |
| Max CIDR per VPC is five. | A VPC can have 5 IPv4 CIDR blocks by default (adjustable up to 50). | It's an adjustable quota. [AWS](https://docs.aws.amazon.com/vpc/latest/userguide/amazon-vpc-limits.html) |
| **Elastic Troughtput** - automatically scales up or down based on our workloads. Used for unpredictable wor... | **Elastic Throughput** - automatically scales up or down based on our workloads. Best for unpredictable workloads. | Typo. [AWS](https://docs.aws.amazon.com/efs/latest/ug/performance.html) |
| **Proactive Controls** act at the time of deployment, | **Proactive controls** act at the time of deployment (using CloudFormation Hooks), | Added the mechanism. |
| It’s not available in all regions. | It’s not available in all regions. CloudShell is on the exam's out-of-scope list. | Exam scope. |
| **AWS SDK** (Protected by access keys) | **AWS SDK** (Protected by access keys, out of scope for the exam) | Exam scope. |

## Structural changes
- **Images removed.** The source used about 260 screenshots, some of which look like course slides, so they weren't copied. Image-only content was rebuilt as tables or Mermaid diagrams, including EC2 instance types, Lambda limits, CloudFront price classes, SQS vs SNS vs Kinesis, Security Groups vs NACLs and the DR comparison.
- **Kinesis Data Analytics for SQL removed.** It shut down on 27 January 2026. The Flink part moved to [[21 Streaming and Data Ingestion|Managed Service for Apache Flink]].
- **`aws-auth` detail removed** from [[18 Containers|EKS Security]] in favour of access entries.
- **Snow Family rewritten.** Device specs for retired models were removed. See [[27 Migration and Data Transfer|AWS Snow Family]].
- **Step Functions Map examples rewritten.** The Distributed mode example used an invalid state type. See [[20 Messaging and Integration|Step Functions Map State]].
- **Duplicate Parameter Store text removed** from Systems Manager.
- **Database summaries** were merged into their service notes.

## Kept after checking
- "Both SQS Standard and FIFO queues can be subscribers" under Amazon SNS is **correct**. AWS docs confirm FIFO topics deliver to both. An earlier review wrongly flagged it.

## Not confirmed against a live AWS page
- Shield Advanced's $3,000 monthly price: the pricing page couldn't be read as text.
- Route 53's $0.50 hosted zone price: not fetched.
- Amazon Linux 2 end-of-support date: not confirmed, so it isn't stated.
- Snowcone: absent from current docs, with no explicit end date found.
- Vendor performance figures such as "up to 10x" are AWS marketing claims.
- KMS custom rotation period range: AWS docs confirm custom periods, but the exact range wasn't extracted, so it isn't stated.


---
**Home:** [[Home]]
