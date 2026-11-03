---
tags: [practice, scope/in]
---

# Practice Exam 4

> [!info] How to sit this exam
> - Set a timer for **130 minutes**, and sit it in one go, with no notes.
> - Write your answers on paper or in another note, and do not open the answers until you finish.
> - There are 65 questions. The real exam has 15 unscored questions, but all of these count here.
> - Score it with the table at the end, then review every question.
> - Aim for **80% or more** (52 of 65). See the [[Study Guide#Step 12 The readiness gate|readiness gate]].
>
> These are original practice questions written for this vault. They are not real exam questions, their difficulty has not been calibrated against the real exam, and real questions are often longer, so expect to do more reading on the day.

**1.** An application is scaled vertically by changing instance size at night, which needs downtime. The team wants to scale without interrupting users. Which change is the most appropriate?

- A. Move to a larger instance permanently
- B. Use a Dedicated Host
- C. Scale horizontally with an Auto Scaling group behind a load balancer
- D. Disable health checks

> [!success]- Answer
> **C.** Horizontal scaling adds capacity without restarts. A larger instance wastes money and still has a limit.
>
> *Task 2.1.* Review: [[31 Architecture Patterns#Horizontal and vertical scaling|Horizontal and vertical scaling]]

**2.** A CloudFront distribution serves dynamic content from an ALB in one Region, and static content from S3. The company wants to survive a Region failure for the application. Which design fits?

- A. Increase the CloudFront TTL to one year
- B. Add more edge locations using a price class
- C. Deploy the application in a second Region, and use an origin group or Route 53 failover to reach it
- D. Enable S3 Transfer Acceleration

> [!success]- Answer
> **C.** A second Region is needed for a Region failure, and failover directs traffic to it. TTLs and price classes do not move dynamic traffic.
>
> *Task 2.2.* Review: [[12 CloudFront and Global Accelerator#Availability|Availability]]

**3.** An API returns the same product list for thousands of requests per second, and the list changes hourly. The team wants to reduce load on the database with the least code change. Which option is best?

- A. Add an SQS queue between the API and the database
- B. Enable Multi-AZ
- C. Add a read replica and rewrite the data layer
- D. Enable API Gateway caching with a suitable TTL

> [!success]- Answer
> **D.** API caching answers repeated requests before they reach the backend, with no code change. A queue does not suit synchronous reads. Multi-AZ does not serve reads.
>
> *Task 2.1.* Review: [[15 ElastiCache and Other Databases#Where caches fit|Where caches fit]]

**4.** An internal microservice needs only TCP forwarding between tiers, with no HTTP features. Which load balancer is the simplest fit?

- A. Application Load Balancer with WAF
- B. Network Load Balancer
- C. CloudFront
- D. Gateway Load Balancer

> [!success]- Answer
> **B.** An NLB handles TCP, with no features that the workload would not use. WAF and CloudFront add cost, and a GWLB is for appliances.
>
> *Task 4.2.* Review: [[05 Load Balancing and Auto Scaling#Choosing a load balancer|Choosing a load balancer]]

**5.** The operations team wants to be notified when an ECS task stops unexpectedly. Which approach is the simplest?

- A. Add an ALB in front of the tasks
- B. Poll the ECS API from a cron job on EC2
- C. Create an EventBridge rule for ECS task state change events, targeting an SNS topic
- D. Check the CloudTrail event history each morning

> [!success]- Answer
> **C.** EventBridge receives task state changes, and it can notify directly. Polling adds work. CloudTrail is not an alerting tool.
>
> *Task 2.1.* Review: [[18 Containers#Event-driven patterns|Event-driven patterns]]

**6.** A team must upgrade a major database version on RDS for PostgreSQL with minimal downtime and an easy way back. Which feature fits?

- A. RDS Blue/Green Deployments
- B. Delete and recreate the database
- C. Change the engine version on the live instance during peak hours
- D. Restore from a cross-Region snapshot

> [!success]- Answer
> **A.** Blue/Green creates a synchronised copy for the upgrade, then switches over quickly.
>
> *Task 4.3.* Review: [[13 RDS and Aurora#Other RDS features|Other RDS features]]

**7.** Field teams upload multi-gigabyte files from across the world to a bucket in one Region. Uploads are slow and fail often. Which two changes improve this? (Choose two.)

- A. Use multipart upload
- B. Enable S3 Transfer Acceleration
- C. Use byte-range fetches
- D. Serve the files through CloudFront signed cookies
- E. Use S3 Standard-IA

> [!success]- Answer
> **A and B.** Acceleration routes through edge locations, and multipart parallelises and allows retries of parts. Byte-range fetches are for downloads. A storage class does not change upload speed.
>
> *Task 3.1.* Review: [[06 Amazon S3#Performance|Performance]]

**8.** A company uses AWS Organizations and wants a standard backup plan applied to all accounts, based on resource tags, with reports showing compliance. Which approach needs the least effort?

- A. Use Data Lifecycle Manager in each account
- B. Use AWS Backup with organisation backup policies, selecting resources by tag
- C. Write a Lambda function in each account
- D. Ask each team to create snapshots by hand

> [!success]- Answer
> **B.** Backup policies in Organizations apply plans across accounts, and tags select resources. The others are per-account and do not cover all services.
>
> *Task 1.3.* Review: [[28 High Availability and Disaster Recovery#AWS Backup|AWS Backup]]

**9.** A company must place a critical workload so that it continues through the failure of a single data centre, at the lowest added cost. Which approach fits?

- A. Deploy across multiple Availability Zones in one Region
- B. Deploy to several instances in one Availability Zone
- C. Deploy in multiple Regions
- D. Use a larger instance with a Dedicated Host

> [!success]- Answer
> **A.** AZs are separate data centres, so Multi-AZ covers this. Multi-Region costs more than the requirement needs. One AZ or one host remains a single point of failure.
>
> *Task 2.2.* Review: [[01 Cloud Foundations#The global infrastructure|The global infrastructure]]

**10.** A company must classify data across its S3 estate on a continuing basis, and feed sensitive-data findings into its central security view. Which combination fits?

- A. Amazon GuardDuty, with findings sent to AWS Budgets
- B. Amazon Macie automated discovery, with findings sent to AWS Security Hub
- C. AWS Glue crawlers, with results sent to Trusted Advisor
- D. Amazon Inspector, with findings sent to AWS Artifact

> [!success]- Answer
> **B.** Macie finds sensitive data, and Security Hub collects findings. The other pairs do not do this.
>
> *Task 1.3.* Review: [[24 Threat Protection and Security Services#Amazon Macie|Amazon Macie]]

**11.** A team can reach a web server on port 443, but a new application port returns a timeout. The application is confirmed to be listening. What is the most likely cause?

- A. The security group or network ACL does not allow the port
- B. The instance has no IAM role
- C. The bucket policy is blocking traffic
- D. The application has crashed

> [!success]- Answer
> **A.** A timeout usually means a firewall is dropping traffic. A crashed application or closed port gives connection refused. IAM and bucket policies do not control network ports.
>
> *Task 1.2.* Review: [[09 VPC Fundamentals#Security groups|Security groups]]

**12.** A company uses AWS Control Tower. It wants to stop a CloudFormation stack from creating an unencrypted RDS instance, before the resource is provisioned. Which kind of control should it use?

- A. A preventive control based on an SCP
- B. A proactive control
- C. A detective control
- D. An IAM Access Analyzer finding

> [!success]- Answer
> **B.** Proactive controls check resources before provisioning, using CloudFormation Hooks. Preventive controls block API actions in general. Detective controls report afterwards. Access Analyzer reports access.
>
> *Task 1.1.* Review: [[03 Multi-Account Governance#AWS Control Tower|AWS Control Tower]]

**13.** A company has existing Spark jobs, and it wants to run them nightly on large datasets in S3, with low cost. Which service fits best?

- A. Amazon Redshift Spectrum
- B. Amazon Athena
- C. AWS Data Pipeline
- D. Amazon EMR with Spot task nodes

> [!success]- Answer
> **D.** EMR runs Spark, and Spot suits task nodes. Athena is SQL-focused. Data Pipeline is closed to new customers.
>
> *Task 3.5.* Review: [[22 Data Lakes and Analytics#Choosing an analytics service|Choosing an analytics service]]

**14.** A bank needs a private connection to AWS that does not use the public internet, with consistent performance, and encryption at layer 2 on a 100 Gbps dedicated link. What should a solutions architect recommend?

- A. AWS Site-to-Site VPN with a large bandwidth tunnel
- B. AWS Client VPN
- C. A hosted Direct Connect connection of 50 Mbps with MACsec
- D. AWS Direct Connect with MACsec

> [!success]- Answer
> **D.** MACsec encrypts at layer 2 on supported dedicated connections. A VPN uses the internet. Client VPN is for users. MACsec is not available on hosted connections.
>
> *Task 1.2.* Review: [[10 VPC Connectivity and Hybrid Networking#AWS Direct Connect|AWS Direct Connect]]

**15.** Developers accidentally overwrite objects in a bucket. The team wants to recover previous versions, with no change to the application. What should it do?

- A. Enable S3 Versioning
- B. Enable S3 Transfer Acceleration
- C. Enable S3 Object Lock in Compliance mode
- D. Enable S3 event notifications

> [!success]- Answer
> **A.** Versioning keeps prior versions on overwrite. Object Lock would stop overwrites of locked versions, and it is much stricter than the need. The others do not keep older data.
>
> *Task 1.3.* Review: [[06 Amazon S3#Versioning|Versioning]]

**16.** A law firm must keep documents for the duration of a court case with no known end date. The documents already have a one-year retention period, which ends soon. Administrators must not be able to delete them, while the case continues. What should a solutions architect do?

- A. Apply an Object Lock legal hold to the objects
- B. Extend versioning
- C. Enable default encryption
- D. Add a lifecycle rule to move them to Glacier

> [!success]- Answer
> **A.** A legal hold has no end date and stays in place until someone with permission removes it. Versioning does not stop deletion of versions. A lifecycle rule moves data and does not protect it.
>
> *Task 1.3.* Review: [[07 S3 Security and Data Protection#S3 Object Lock|S3 Object Lock]]

**17.** A company wants to run containers on its own on-premises servers, using the same control plane and APIs as its ECS services in AWS. Which option fits?

- A. Amazon EKS Distro
- B. Amazon ECS Anywhere
- C. AWS Elastic Beanstalk
- D. AWS Fargate

> [!success]- Answer
> **B.** ECS Anywhere runs tasks on your servers, with the control plane in AWS. Fargate runs in AWS. EKS Distro is a Kubernetes distribution you run yourself.
>
> *Task 2.1.* Review: [[18 Containers#Where tasks run|Where tasks run]]

**18.** A company wants monthly storage costs broken down by project. Tags already exist on all buckets. Costs are not appearing by tag. What is the most likely fix?

- A. Add the tags to each object
- B. Enable S3 Versioning
- C. Enable AWS Config
- D. Activate the tags as cost allocation tags in the Billing console

> [!success]- Answer
> **D.** Tags must be activated before they appear in cost reports. The others do not affect billing reports.
>
> *Task 4.1.* Review: [[29 Cost Optimisation#Cost allocation tags|Cost allocation tags]]

**19.** A legacy application cannot be changed, and it opens many short-lived database connections. Which two services improve its reliability, with no code changes? (Choose two.)

- A. DynamoDB global tables
- B. Amazon RDS Proxy
- C. Amazon Kinesis Data Streams
- D. RDS Multi-AZ
- E. Amazon API Gateway

> [!success]- Answer
> **B and D.** RDS Proxy pools connections and Multi-AZ adds failover, and both are transparent to the application. The others would need rewrites.
>
> *Task 2.2.* Review: [[28 High Availability and Disaster Recovery#Making legacy applications more reliable|Making legacy applications more reliable]]

**20.** An application uses a third-party API key, not a database password. The team needs the key encrypted, versioned, cheap, and readable by one IAM role. Automatic rotation is not needed. Which option is the most cost-effective?

- A. A SecureString parameter in Parameter Store, standard tier
- B. An environment variable in the task definition
- C. An S3 bucket with public access blocked, and an access key
- D. AWS Secrets Manager with a rotation Lambda function

> [!success]- Answer
> **A.** A SecureString is encrypted with KMS and has no extra charge on the standard tier. Secrets Manager adds a per-secret cost that is justified by rotation. An access key is the wrong pattern, and an environment variable is visible to anyone who can read the definition.
>
> *Task 1.2.* Review: [[23 Encryption and Secrets#Secrets Manager and Parameter Store|Secrets Manager and Parameter Store]]

**21.** An application runs in two Regions, and it should serve each user from the lowest-latency Region. If a Region becomes unhealthy, traffic should move to the other. Which Route 53 configuration fits?

- A. Simple routing with two values
- B. Latency routing with health checks
- C. Geolocation routing with no default record
- D. Weighted routing with zero weights

> [!success]- Answer
> **B.** Latency routing picks the fastest Region, and health checks remove unhealthy ones. Simple routing cannot use health checks. Geolocation does not optimise for latency.
>
> *Task 2.2.* Review: [[11 Route 53#Routing policies|Routing policies]]

**22.** A company's data lake must meet these rules: data is encrypted at rest, access is logged, and only specific columns are visible to some users. Which combination should a solutions architect use?

- A. SSE-C, CloudWatch metrics and bucket tags
- B. No encryption, Athena workgroups and IAM users
- C. SSE-S3, VPC Flow Logs and S3 ACLs
- D. SSE-KMS on the bucket, CloudTrail logging, and Lake Formation column permissions

> [!success]- Answer
> **D.** This combination meets each of the rules. Flow logs do not record object access. ACLs cannot control columns.
>
> *Task 1.3.* Review: [[22 Data Lakes and Analytics#Securing a data lake|Securing a data lake]]

**23.** A company uses a cross-Region read replica for DR on RDS for PostgreSQL. What must happen during a disaster to make the replica writable?

- A. The replica must be restored from S3
- B. The replica must be promoted to a standalone database, and the application pointed at it
- C. Nothing, because failover is automatic
- D. The replica must be rebooted with Multi-AZ on

> [!success]- Answer
> **B.** Promotion is a manual step, and the replica then has its own endpoint. Multi-AZ failover is automatic, and that is a separate feature.
>
> *Task 2.2.* Review: [[13 RDS and Aurora#Read replicas|Read replicas]]

**24.** A distributed database replicates its data across nodes, and it needs the highest possible local disk performance. Data on one node can be rebuilt from the others. Which storage is the best fit?

- A. EBS sc1
- B. Amazon S3
- C. Amazon EFS
- D. EC2 instance store

> [!success]- Answer
> **D.** Instance store gives the highest local I/O, and the replication protects the data. sc1 is slow. S3 and EFS are network storage.
>
> *Task 3.1.* Review: [[08 Block and File Storage#EC2 instance store|EC2 instance store]]

**25.** A team is choosing databases for a new platform: (1) a MongoDB-based product catalogue, and (2) a Cassandra-based event log. They want managed services with minimal application change. Which pair fits?

- A. Amazon Neptune and Amazon RDS
- B. Amazon DocumentDB and Amazon Keyspaces
- C. Amazon Redshift and Amazon DocumentDB
- D. Amazon Keyspaces and Amazon Neptune

> [!success]- Answer
> **B.** DocumentDB is MongoDB compatible, and Keyspaces is Cassandra compatible.
>
> *Task 3.3.* Review: [[15 ElastiCache and Other Databases#Choosing a database|Choosing a database]]

**26.** A CI system runs builds that can be retried, across several instance types. It wants the most savings, with few interruptions. Which option fits?

- A. Spot Instances with the `price-capacity-optimized` allocation strategy across several instance types
- B. Spot Instances in a single instance type and AZ
- C. Dedicated Instances
- D. On-Demand Instances with Compute Savings Plans

> [!success]- Answer
> **A.** Diversifying with this strategy reduces interruptions at a low price. A single pool has more risk. The others cost more.
>
> *Task 4.2.* Review: [[04 Amazon EC2#Spot Instances|Spot Instances]]

**27.** A retailer's RTO is one hour and its RPO is five minutes. Data must replicate all the time, but the company wants to avoid paying for application servers in the DR Region. Which strategy fits?

- A. Warm standby
- B. Backup and restore
- C. Pilot light
- D. Multi-site active-active

> [!success]- Answer
> **C.** Pilot light replicates the data, and it leaves compute off until needed. Backup and restore would struggle to meet the RPO. Warm standby and active-active run servers all the time.
>
> *Task 2.2.* Review: [[28 High Availability and Disaster Recovery#Disaster recovery strategies|Disaster recovery strategies]]

**28.** A company stores 200 TB of cold log data on EBS for a rarely used application that needs block storage. Performance is not important. Which volume type is cheapest?

- A. sc1
- B. st1
- C. gp3
- D. io2

> [!success]- Answer
> **A.** sc1 is the lowest-cost EBS volume, for cold data. st1 is for frequently accessed throughput. SSD types cost more.
>
> *Task 4.1.* Review: [[08 Block and File Storage#Volume types|Volume types]]

**29.** A stream receives 12 MB/s of records. Each provisioned shard accepts 1 MB/s. The team also wants room for a 50% peak. How many shards should it plan for?

- A. 12
- B. 18
- C. 24
- D. 6

> [!success]- Answer
> **B.** 12 MB/s at 1.5 times is 18 MB/s, which needs 18 shards. 12 shards would have no room for peaks.
>
> *Task 3.5.* Review: [[21 Streaming and Data Ingestion#Sizes and speeds|Sizes and speeds]]

**30.** Applications in a VPC must resolve names in an on-premises domain over a Direct Connect link, and on-premises servers must resolve private AWS names. What should a solutions architect configure?

- A. A public hosted zone for each domain
- B. Route 53 Resolver outbound and inbound endpoints, with forwarding rules
- C. A multivalue answer record
- D. A CNAME at the zone apex

> [!success]- Answer
> **B.** Outbound endpoints send queries to on-premises, and inbound endpoints receive them. Public zones expose names to the internet.
>
> *Task 3.4.* Review: [[11 Route 53#Hybrid DNS with Route 53 Resolver|Hybrid DNS with Route 53 Resolver]]

**31.** A company must make sure that its DR environment can be rebuilt exactly, in any Region, from a tested definition. Which approach fits?

- A. Take screenshots of each resource
- B. Keep a Word document of console steps
- C. Rely on AWS Support to rebuild it
- D. Define the infrastructure in CloudFormation templates, and test them regularly

> [!success]- Answer
> **D.** Infrastructure as code is repeatable and testable. Manual steps drift and fail under pressure.
>
> *Task 2.2.* Review: [[26 Infrastructure as Code and Operations#AWS CloudFormation|AWS CloudFormation]]

**32.** A startup has a simple web app and wants to deploy from source code with load balancing and scaling handled for it, while still being able to change the underlying instances. Which service fits best?

- A. AWS Batch
- B. AWS Outposts
- C. AWS Elastic Beanstalk
- D. Amazon EKS on EC2

> [!success]- Answer
> **C.** Beanstalk handles deployment, load balancing and scaling, and it keeps resources accessible. EKS adds Kubernetes work. Batch is for jobs. Outposts are on-premises.
>
> *Task 2.1.* Review: [[19 Other Compute Services#Choosing compute|Choosing compute]]

**33.** A company wants one service for each need: (1) a queue for background jobs, and (2) real-time clickstream analysis by several applications with replay. Which pair fits?

- A. Amazon SNS for jobs, and Amazon SQS for clickstream
- B. Amazon Kinesis for jobs, and Amazon MQ for clickstream
- C. Amazon SQS for jobs, and Kinesis Data Streams for clickstream
- D. AWS Step Functions for jobs, and AWS AppFlow for clickstream

> [!success]- Answer
> **C.** SQS buffers jobs for workers, and Kinesis allows many readers and replay. The other pairs mismatch the needs.
>
> *Task 2.1.* Review: [[20 Messaging and Integration#Why decouple|Why decouple]]

**34.** A company must keep recreated image previews for 90 days, read rarely, and it is fine to lose them. Which is the most cost-effective S3 class?

- A. S3 Standard-IA
- B. S3 Glacier Deep Archive
- C. S3 One Zone-IA
- D. S3 Standard

> [!success]- Answer
> **C.** One Zone-IA costs 20% less than Standard-IA, and the risk of loss is acceptable for data that can be recreated. S3 Standard costs more for data that is read rarely. Deep Archive has a 180-day minimum and slow retrieval.
>
> *Task 4.1.* Review: [[06 Amazon S3#Storage classes|Storage classes]]

**35.** A company wants on-premises servers to call AWS APIs without storing long-term access keys. The servers already have X.509 certificates from an internal CA. What should a solutions architect recommend?

- A. Cognito identity pools
- B. IAM Roles Anywhere
- C. An IAM user with keys rotated weekly
- D. EC2 instance profiles on the on-premises servers

> [!success]- Answer
> **B.** Roles Anywhere exchanges a certificate for temporary credentials. Rotated keys are still long-term keys. Instance profiles exist only on EC2. Cognito is for app users.
>
> *Task 1.1.* Review: [[02 IAM and Federation#Roles and temporary credentials|Roles and temporary credentials]]

**36.** A company runs a ZFS file server for Linux clients, with heavy use of snapshots and clones, and it wants a managed service with very high IOPS. Which service fits?

- A. Amazon S3 File Gateway
- B. Amazon FSx for Windows File Server
- C. Amazon FSx for OpenZFS
- D. Amazon EBS st1

> [!success]- Answer
> **C.** FSx for OpenZFS is the managed equivalent. The others use different protocols or do not offer these features.
>
> *Task 3.1.* Review: [[08 Block and File Storage#FSx for OpenZFS|FSx for OpenZFS]]

**37.** A company wants container images to be scanned for known vulnerabilities as they are pushed, and it wants Lambda functions scanned on deployment. Which service should it use?

- A. Amazon Inspector
- B. AWS Trusted Advisor
- C. Amazon Macie
- D. Amazon GuardDuty

> [!success]- Answer
> **A.** Inspector scans ECR images, Lambda functions and EC2 instances for CVEs. GuardDuty detects threats in logs. Macie finds sensitive data. Trusted Advisor gives general recommendations.
>
> *Task 1.2.* Review: [[24 Threat Protection and Security Services#Amazon Inspector|Amazon Inspector]]

**38.** A company has 12 standalone AWS accounts. It wants one bill, shared Savings Plan discounts, and a way to apply policies to groups of accounts. What should a solutions architect do first?

- A. Set up Cost Explorer in each account, and export the data
- B. Create an IAM role in each account that trusts the finance account
- C. Use AWS Control Tower in each account separately
- D. Create an organisation in AWS Organizations with all features enabled, and invite the accounts

> [!success]- Answer
> **D.** Organizations gives consolidated billing, shared discounts and policies. IAM roles do not join billing. Control Tower manages one organisation, and it is not run per account. Cost Explorer only reports.
>
> *Task 1.1.* Review: [[03 Multi-Account Governance#AWS Organizations|AWS Organizations]]

**39.** A public API is being overused by one client, which drives up Lambda and data costs. Which change limits that client's request rate without affecting other clients?

- A. Remove the API's custom domain
- B. Add an API Gateway usage plan with a throttle and quota for that client
- C. Reduce Lambda memory for all clients
- D. Add a NAT gateway

> [!success]- Answer
> **B.** A usage plan limits one client. The others do not target the client, and lowering memory affects everyone.
>
> *Task 4.4.* Review: [[17 API Gateway and Front-End Services#Throttling and usage plans|Throttling and usage plans]]

**40.** A role in Account A has an identity policy that allows `s3:GetObject` on a bucket in Account B. The bucket has no bucket policy, and neither account has an SCP that restricts S3. Calls from the role fail with `AccessDenied`. What should a solutions architect do?

- A. Turn off Block Public Access on the bucket
- B. Add a bucket policy in Account B that allows the role to read objects
- C. Add `s3:*` to the role's identity policy
- D. Enable ACLs on the bucket for all users

> [!success]- Answer
> **B.** Cross-account access needs both sides to allow the action, and here the bucket's account has not. More identity permissions do not help. ACLs and Block Public Access are not the right tools, and neither should be loosened for this.
>
> *Task 1.1.* Review: [[02 IAM and Federation#Policy evaluation logic|Policy evaluation logic]]

**41.** An application in Account B must decrypt S3 objects encrypted with a customer managed KMS key in Account A. The S3 bucket policy already allows the read. What else is required? (Choose two.)

- A. Share the key material as a file
- B. Copy the key to Account B
- C. Allow Account B in the KMS key policy
- D. Allow `kms:Decrypt` on the key in an IAM policy in Account B
- E. Convert the bucket to SSE-S3

> [!success]- Answer
> **C and D.** Cross-account KMS use needs the key policy and an IAM policy in the calling account. Key material is never shared that way. KMS keys cannot be copied.
>
> *Task 1.3.* Review: [[23 Encryption and Secrets#Key policies|Key policies]]

**42.** An image thumbnail service runs on a steady, very high volume, all day, on Lambda. A cost review shows that EC2 would be cheaper. When can this conclusion be right?

- A. Only when functions run under 100 ms
- B. When traffic is steady and high enough that always-on capacity costs less than per-request charges
- C. Never, because Lambda is always cheaper
- D. Only when the functions use Python

> [!success]- Answer
> **B.** Serverless pricing suits spiky or low traffic. With very high steady use, reserved compute can cost less.
>
> *Task 4.2.* Review: [[16 Lambda and Serverless#When to use serverless|When to use serverless]]

**43.** An organisation lets a platform team create IAM users for contractors. The contractors must never exceed a fixed set of permissions, whatever policies are attached later. Which control fits a single identity rather than a whole account?

- A. An SCP on the account
- B. A permission boundary on each contractor user
- C. A resource control policy on the account
- D. A tag policy on the organisation

> [!success]- Answer
> **B.** Boundaries set a ceiling for one user or role. SCPs and RCPs apply to a whole account or OU. Tag policies standardise tags.
>
> *Task 1.1.* Review: [[02 IAM and Federation#Permission boundaries|Permission boundaries]]

**44.** A company is designing a new three-tier web application. Which two choices improve loose coupling and independent scaling? (Choose two.)

- A. Store session data on the web servers
- B. Have the processing tier connect to specific web server IP addresses
- C. Place an SQS queue between the web tier and the processing tier
- D. Use a single EC2 instance for all three tiers
- E. Place an Application Load Balancer between users and the web tier

> [!success]- Answer
> **C and E.** Load balancers and queues hide individual instances. The others tie components together.
>
> *Task 2.1.* Review: [[31 Architecture Patterns#Multi-tier architecture|Multi-tier architecture]]

**45.** A company wants to move an RDS for MySQL database to Aurora MySQL with little downtime. Which approach fits?

- A. Use AWS Snowball Edge
- B. Move the data to DynamoDB first
- C. Create an Aurora read replica of the RDS instance, then promote it when replication lag reaches zero
- D. Dump the database to a CSV file and re-enter it

> [!success]- Answer
> **C.** An Aurora read replica keeps the data in step until cutover. The other options cause long downtime, or they do not apply.
>
> *Task 4.3.* Review: [[27 Migration and Data Transfer#Moving to Aurora|Moving to Aurora]]

**46.** A compliance officer asks for AWS's latest SOC 2 report and for evidence that the company's own S3 buckets are not public. Which two services provide these? (Choose two.)

- A. AWS Config for the evidence about the company's buckets
- B. AWS Direct Connect for the evidence
- C. Amazon Macie for the SOC 2 report
- D. AWS Artifact for the SOC 2 report
- E. Amazon GuardDuty for the SOC 2 report

> [!success]- Answer
> **A and D.** Artifact provides AWS's reports, and Config evaluates your own resources. The others do not provide these.
>
> *Task 1.2.* Review: [[24 Threat Protection and Security Services#Compliance in practice|Compliance in practice]]

**47.** A partner needs access to one internal application in a VPC. Its network overlaps with the company's. No other access may be granted. What should a solutions architect use?

- A. AWS PrivateLink with a Network Load Balancer
- B. VPC peering
- C. Transit Gateway
- D. A Site-to-Site VPN with full routing

> [!success]- Answer
> **A.** PrivateLink exposes one service and allows overlapping CIDRs. Peering and Transit Gateway need non-overlapping ranges and expose more.
>
> *Task 3.4.* Review: [[10 VPC Connectivity and Hybrid Networking#Choosing a connection|Choosing a connection]]

**48.** A new consumer app has unknown traffic for its launch. The team wants no capacity planning. After a few months the pattern will be clear and steady. What is the most cost-effective plan?

- A. Start with DynamoDB on-demand, and switch to provisioned with auto scaling when traffic becomes predictable
- B. Use a global table in three Regions from the start
- C. Use on-demand forever, because it is always cheapest
- D. Start provisioned for peak, and keep it

> [!success]- Answer
> **A.** On-demand handles the unknown, and provisioned suits steady traffic later. You can switch between modes.
>
> *Task 4.3.* Review: [[14 DynamoDB#Capacity modes|Capacity modes]]

**49.** A company uses Okta for its workforce and has 25 AWS accounts. It wants users and groups to appear in AWS automatically when they change in Okta, with access assigned by job function. What should a solutions architect recommend? (Choose two.)

- A. Create IAM users in each account, using a script
- B. Use IAM Identity Center with Okta as an external identity provider, with SCIM provisioning
- C. Use AWS Directory Service Simple AD
- D. Create permission sets for each job function, and assign them to groups in each account
- E. Use Amazon Cognito identity pools for the employees

> [!success]- Answer
> **B and D.** Identity Center connects to Okta, SCIM keeps identities in step, and permission sets map job functions to accounts. Scripts creating IAM users are hard to run and audit. Cognito is for customers. Simple AD is closed to new customers.
>
> *Task 1.1.* Review: [[02 IAM and Federation#AWS IAM Identity Center|AWS IAM Identity Center]]

**50.** Instances in an Auto Scaling group take 10 minutes to bootstrap, and sudden spikes cause errors. The team wants new capacity in seconds, at a low cost while idle. Which feature fits?

- A. A larger launch template
- B. A warm pool of stopped, pre-initialised instances
- C. A longer cooldown period
- D. Reserved Instances

> [!success]- Answer
> **B.** Warm pools keep initialised instances ready to start quickly. Cooldown slows scaling further. Reserved Instances are a billing feature.
>
> *Task 3.2.* Review: [[05 Load Balancing and Auto Scaling#Warm pools|Warm pools]]

**51.** A public API on API Gateway calls a Lambda function that sometimes takes more than five minutes. Clients receive timeouts. Which design change is best?

- A. Use a WebSocket connection for all clients, and leave the function unchanged
- B. Add more memory to the function
- C. Return 202 Accepted, place the work on a queue or start a Step Functions workflow, and let clients fetch the result later
- D. Enable API Gateway caching

> [!success]- Answer
> **C.** Long-running work should be asynchronous. More memory may help a little, but it does not fix the design. Caching does not help with a new request. WebSockets add complexity without solving the timing.
>
> *Task 2.1.* Review: [[17 API Gateway and Front-End Services#Limits|Limits]]

**52.** A company needs Direct Connect bandwidth of 2 Gbps today, with possible growth. It is happy to work through a partner, and it wants to avoid over-buying a 10 Gbps port. Which option fits?

- A. Site-to-Site VPN over the internet at 1.25 Gbps
- B. A LAG of four 100 Gbps connections
- C. A hosted connection at the required speed
- D. A dedicated 400 Gbps connection

> [!success]- Answer
> **C.** Hosted connections come in sizes from 50 Mbps to 25 Gbps through partners. The others are far larger or do not meet the need.
>
> *Task 4.4.* Review: [[10 VPC Connectivity and Hybrid Networking#Connection types|Connection types]]

**53.** A game publisher wants to speed up two things worldwide: downloads of large static patches, and real-time game traffic over UDP. Which two choices should it make? (Choose two.)

- A. Amazon CloudFront for the patches
- B. Amazon CloudFront for the UDP game traffic
- C. S3 Transfer Acceleration for player downloads
- D. AWS Global Accelerator for the game traffic
- E. AWS Direct Connect for each player

> [!success]- Answer
> **A and D.** CloudFront caches static downloads, and Global Accelerator carries UDP over the AWS network. CloudFront does not handle UDP. Transfer Acceleration is designed for uploads into a bucket. Direct Connect is for fixed sites and not for players.
>
> *Task 2.1.* Review: [[12 CloudFront and Global Accelerator#Choosing between them|Choosing between them]]

**54.** A bank exchanges files with partners using AS2 and SFTP, and it wants the files in S3, with no servers to manage. Which service fits?

- A. AWS Transfer Family
- B. AWS Snow Family
- C. Amazon AppFlow
- D. AWS DataSync

> [!success]- Answer
> **A.** Transfer Family supports SFTP, FTPS, FTP and AS2. DataSync moves storage between locations. AppFlow connects SaaS applications.
>
> *Task 3.5.* Review: [[27 Migration and Data Transfer#AWS Transfer Family|AWS Transfer Family]]

**55.** A company serves a web application through CloudFront with an internet-facing ALB origin. It wants to stop anyone going straight to the ALB. Which approach works?

- A. Use a Network ACL that allows only the users' IP addresses
- B. Have CloudFront add a secret custom header, and have the ALB reject requests without it, and limit the ALB to CloudFront's prefix list
- C. Use S3 Origin Access Control on the ALB
- D. Enable sticky sessions on the ALB

> [!success]- Answer
> **B.** A secret header plus the managed prefix list limits access to CloudFront. OAC is for S3 and some other origins, and not this pattern. Users' addresses do not reach the ALB through CloudFront. Stickiness has no security effect. VPC origins are another good option if the ALB can be private.
>
> *Task 1.2.* Review: [[12 CloudFront and Global Accelerator#Protecting other origins|Protecting other origins]]

**56.** A team needs to choose a compute service for a containerised genomics pipeline that runs for many hours. Jobs need GPU instances at times, and queues should be managed for them. Which service fits?

- A. AWS Lambda
- B. Amazon API Gateway
- C. AWS Batch
- D. AWS Fargate alone

> [!success]- Answer
> **C.** Batch runs long jobs, manages queues, and can use GPU instances on EC2. Lambda stops at 15 minutes. Fargate does not offer GPUs.
>
> *Task 3.2.* Review: [[19 Other Compute Services#AWS Batch|AWS Batch]]

**57.** A clustered application needs a shared block device in one AZ, and it has its own cluster-aware storage layer. The team wants high availability against an instance failure. Which option fits?

- A. Instance store volumes
- B. st1 volumes shared by NFS
- C. gp3 volumes with Multi-Attach
- D. io2 volumes with Multi-Attach on Nitro instances

> [!success]- Answer
> **D.** Multi-Attach needs io1 or io2. gp3 does not support it. Instance store cannot be shared.
>
> *Task 2.2.* Review: [[08 Block and File Storage#Multi-Attach|Multi-Attach]]

**58.** An application reads from a global secondary index and sometimes misses an item that was just written. It must always read the latest data. What should a solutions architect do?

- A. Request a strongly consistent read on the GSI
- B. Add more GSIs
- C. Enable TTL
- D. Read from the base table with a strongly consistent read

> [!success]- Answer
> **D.** GSIs support only eventually consistent reads. Strongly consistent reads work on the table and on LSIs.
>
> *Task 3.3.* Review: [[14 DynamoDB#Read consistency|Read consistency]]

**59.** A serverless application on Lambda connects to Aurora, and it must use IAM authentication and handle many concurrent invocations. Which solution fits?

- A. Connect through RDS Proxy with IAM authentication, from a Lambda function in the VPC
- B. Store the password in a Lambda environment variable
- C. Give the Aurora cluster a public endpoint
- D. Increase the Lambda timeout to 15 minutes

> [!success]- Answer
> **A.** RDS Proxy pools connections and supports IAM authentication, and it is reached from within the VPC. Public endpoints and stored passwords lower security.
>
> *Task 3.3.* Review: [[13 RDS and Aurora#RDS Proxy|RDS Proxy]]

**60.** An operations team wants an automated runbook to start when AWS schedules maintenance on one of its instances. Which approach fits?

- A. AWS Trusted Advisor checks
- B. A CloudWatch metric filter on application logs
- C. An EventBridge rule on AWS Health events, which starts a Systems Manager Automation runbook
- D. An AWS Budgets action

> [!success]- Answer
> **C.** AWS Health events describe maintenance that affects you, and EventBridge can start automation. The others do not track this.
>
> *Task 2.2.* Review: [[25 Monitoring and Auditing#AWS Health Dashboard|AWS Health Dashboard]]

**61.** A long-running application takes 30 minutes to load data into memory. Instances are stopped nightly. Users want it ready immediately every morning. What should a solutions architect do?

- A. Stop the instances as usual, and use a larger root volume
- B. Use Spot Instances
- C. Use instance store for the root volume
- D. Launch the instances with hibernation enabled and an encrypted EBS root volume, and hibernate them at night

> [!success]- Answer
> **D.** Hibernation restores memory from the EBS root volume. A larger volume does not keep memory. Instance store roots cannot hibernate.
>
> *Task 3.2.* Review: [[04 Amazon EC2#Hibernation|Hibernation]]

**62.** A network team must carve a VPC into subnets. One subnet must hold 250 EC2 instances, and nothing else. What is the smallest subnet that will work?

- A. /25
- B. /26
- C. /24
- D. /23

> [!success]- Answer
> **C.** A /24 has 256 addresses, and AWS reserves 5, which leaves 251. A /25 leaves only 123, and a /26 leaves 59. A /23 would work, but it is larger than needed.
>
> *Task 3.4.* Review: [[09 VPC Fundamentals#IP addressing and CIDR|IP addressing and CIDR]]

**63.** A company's users are all in Europe and North America, and it wants to reduce CloudFront costs. Which option fits?

- A. Use Price Class 100
- B. Use Price Class All
- C. Enable Origin Shield
- D. Use Lambda@Edge

> [!success]- Answer
> **A.** Price Class 100 limits delivery to the cheapest edge locations. The other options add cost.
>
> *Task 4.4.* Review: [[12 CloudFront and Global Accelerator#Price classes and pricing plans|Price classes and pricing plans]]

**64.** A DynamoDB table must be reachable from a private subnet without internet access, and the team wants no extra cost. What should a solutions architect create?

- A. An internet gateway
- B. A NAT gateway
- C. A gateway VPC endpoint for DynamoDB
- D. An interface VPC endpoint for DynamoDB

> [!success]- Answer
> **C.** Gateway endpoints are free and private. An interface endpoint would also work, but it costs money. NAT and an internet gateway need internet access.
>
> *Task 1.2.* Review: [[14 DynamoDB#Security|Security]]

**65.** A company wants to keep using its backup software, and to stop buying tapes, at the lowest storage cost for backups kept for years. Which solution fits?

- A. Tape Gateway, with tapes archived to S3 Glacier Deep Archive
- B. Volume Gateway stored mode, keeping everything local
- C. Amazon EFS with Standard storage
- D. S3 File Gateway with S3 Standard

> [!success]- Answer
> **A.** Tape Gateway fits existing software, and Deep Archive has the lowest cost. The others either change the workflow or cost more.
>
> *Task 4.1.* Review: [[27 Migration and Data Transfer#AWS Storage Gateway|AWS Storage Gateway]]

## Score your exam

Mark your answers with the key, then count your correct answers for each domain.

> [!example]- Answer key
> 1: C · 2: C · 3: D · 4: B · 5: C · 6: A · 7: A, B · 8: B · 9: A · 10: B  
> 11: A · 12: B · 13: D · 14: D · 15: A · 16: A · 17: B · 18: D · 19: B, D · 20: A  
> 21: B · 22: D · 23: B · 24: D · 25: B · 26: A · 27: C · 28: A · 29: B · 30: B  
> 31: D · 32: C · 33: C · 34: C · 35: B · 36: C · 37: A · 38: D · 39: B · 40: B  
> 41: C, D · 42: B · 43: B · 44: C, E · 45: C · 46: A, D · 47: A · 48: A · 49: B, D · 50: B  
> 51: C · 52: C · 53: A, D · 54: A · 55: B · 56: C · 57: D · 58: D · 59: A · 60: C  
> 61: D · 62: C · 63: A · 64: C · 65: A  

| Domain | Questions | Your score |
| --- | --- | --- |
| Domain 1: Secure | 8, 9, 10, 11, 12, 14, 15, 16, 20, 22, 35, 37, 38, 40, 41, 43, 46, 49, 55, 64 | ___ / 20 |
| Domain 2: Resilient | 1, 2, 3, 5, 17, 19, 21, 23, 27, 31, 32, 33, 44, 51, 53, 57, 60 | ___ / 17 |
| Domain 3: High-Performing | 7, 13, 24, 25, 29, 30, 36, 47, 50, 54, 56, 58, 59, 61, 62 | ___ / 15 |
| Domain 4: Cost-Optimized | 4, 6, 18, 26, 28, 34, 39, 42, 45, 48, 52, 63, 65 | ___ / 13 |
| **Total** | | **___ / 65** |

Add your result to the table in the [[Study Guide#Tracking your progress|Study Guide]], and every mistake to the [[Mistake Log]].

---
**Previous:** [[Practice Exam 3]] · **Next:** [[Practice Exam 5]] · **Plan:** [[Study Guide]]
