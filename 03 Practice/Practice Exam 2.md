---
tags: [practice, scope/in]
---

# Practice Exam 2

> [!info] How to sit this exam
> - Set a timer for **130 minutes**, and sit it in one go, with no notes.
> - Write your answers on paper or in another note, and do not open the answers until you finish.
> - There are 65 questions. The real exam has 15 unscored questions, but all of these count here.
> - Score it with the table at the end, then review every question.
> - Aim for **80% or more** (52 of 65). See the [[Study Guide#Step 12 The readiness gate|readiness gate]].
>
> These are original practice questions written for this vault. They are not real exam questions, their difficulty has not been calibrated against the real exam, and real questions are often longer, so expect to do more reading on the day.

**1.** A development VPC has private subnets in two AZs. Availability is not important, and cost is. Which NAT design is the most cost-effective?

- A. One NAT gateway in each AZ
- B. Transit Gateway with an inspection VPC
- C. A NAT gateway in each subnet
- D. A single NAT gateway shared by both AZs

> [!success]- Answer
> **D.** One shared gateway has the lowest hourly cost, and this environment can accept the risk. One per AZ suits production. The others add cost without benefit here.
>
> *Task 4.4.* Review: [[09 VPC Fundamentals#NAT gateway|NAT gateway]]

**2.** A table has `customer_id` as its partition key. A new feature must look up orders by `order_date` across all customers. The table already holds data. What should a solutions architect do?

- A. Add a local secondary index on `order_date`
- B. Scan the whole table for each request
- C. Export the table to S3 for each lookup
- D. Add a global secondary index with `order_date` in its key

> [!success]- Answer
> **D.** A GSI can have a different partition key, and it can be added at any time. An LSI needs the same partition key and must be created with the table. Scans are slow and costly.
>
> *Task 3.3.* Review: [[14 DynamoDB#Indexes|Indexes]]

**3.** An application stores user uploads, which are served to browsers directly, and it must scale to billions of objects with no capacity planning. Which storage type fits?

- A. Instance store
- B. File storage on Amazon EFS
- C. Object storage on Amazon S3
- D. Block storage on Amazon EBS

> [!success]- Answer
> **C.** S3 scales without limit, and it serves objects over HTTP. EBS is attached to instances and sized in advance. EFS is a file system, not a direct web origin. Instance store is temporary.
>
> *Task 2.1.* Review: [[08 Block and File Storage#Three kinds of storage|Three kinds of storage]]

**4.** A content management system on Linux runs across AZs, and traffic to its shared file system is spiky and hard to predict. Which configuration requires the least tuning?

- A. Amazon EFS with Elastic throughput
- B. EBS gp3 with Multi-Attach
- C. Amazon EFS with Provisioned throughput set for peak
- D. FSx for Windows File Server

> [!success]- Answer
> **A.** Elastic throughput scales automatically with spiky demand. Provisioned means paying for peak. Multi-Attach needs io1 or io2 in one AZ. FSx for Windows suits SMB and Windows.
>
> *Task 3.1.* Review: [[08 Block and File Storage#Amazon EFS|Amazon EFS]]

**5.** An online store needs to recommend products based on who bought what, through multi-hop relationship queries across billions of edges. Which database fits?

- A. Amazon RDS for MySQL
- B. Amazon Redshift
- C. Amazon Neptune
- D. Amazon Keyspaces

> [!success]- Answer
> **C.** Neptune is a graph database, built for relationship queries. Redshift is for analytics. Multi-hop joins are slow on relational engines. Keyspaces is a wide-column database.
>
> *Task 3.3.* Review: [[15 ElastiCache and Other Databases#Choosing a database|Choosing a database]]

**6.** A site has a large, regular traffic increase each weekday morning, and instances take several minutes to start. The team wants capacity ready before the increase, without hand-written schedules for each change in the pattern. Which option fits best?

- A. Manual scaling
- B. Predictive scaling
- C. Lifecycle hooks only
- D. Simple scaling on CPU

> [!success]- Answer
> **B.** Predictive scaling forecasts recurring patterns and scales ahead of them. Simple scaling reacts after the load arrives. Manual scaling needs a person. Hooks do not scale anything.
>
> *Task 3.2.* Review: [[05 Load Balancing and Auto Scaling#Scaling policies|Scaling policies]]

**7.** Executives need interactive dashboards built on data in Redshift and Athena, with no servers to manage. Which service fits?

- A. AWS Glue
- B. Amazon EMR
- C. Amazon Quick
- D. AWS Lake Formation

> [!success]- Answer
> **C.** Amazon Quick provides business intelligence dashboards. Glue prepares data. EMR processes it. Lake Formation secures it.
>
> *Task 3.5.* Review: [[22 Data Lakes and Analytics#Amazon Quick|Amazon Quick]]

**8.** A research institute shares a large public dataset in S3, and wants the organisations that download it to pay for the transfer. Which feature fits?

- A. S3 Storage Lens
- B. S3 Access Points
- C. S3 Object Lock
- D. S3 Requester Pays

> [!success]- Answer
> **D.** With Requester Pays, the authenticated requester pays for requests and data transfer. The others do not change who pays.
>
> *Task 4.1.* Review: [[06 Amazon S3#Other features|Other features]]

**9.** A company's public application behind an ALB and CloudFront suffered a large DDoS attack, and its costs rose sharply. It wants 24/7 access to DDoS experts and financial protection against scaling charges from future attacks. What should it use?

- A. Amazon GuardDuty
- B. AWS Shield Standard
- C. AWS Shield Advanced
- D. AWS Firewall Manager alone

> [!success]- Answer
> **C.** Shield Advanced adds the response team and cost protection. Shield Standard is automatic and has neither. GuardDuty detects threats. Firewall Manager applies rules centrally, and it does not provide DDoS expertise.
>
> *Task 1.2.* Review: [[24 Threat Protection and Security Services#AWS Shield|AWS Shield]]

**10.** Remote employees must reach private applications in a VPC from their laptops, using their corporate identity provider. No office network is involved. What should a solutions architect recommend?

- A. AWS Site-to-Site VPN
- B. AWS Client VPN with SAML federation
- C. Public IP addresses on the applications, with security group rules for each home IP
- D. AWS Direct Connect

> [!success]- Answer
> **B.** Client VPN is built for individual users, and it supports SAML. Site-to-Site connects networks. Direct Connect is a physical link to a data centre. Exposing applications publicly is less secure and hard to manage.
>
> *Task 1.2.* Review: [[10 VPC Connectivity and Hybrid Networking#AWS Client VPN|AWS Client VPN]]

**11.** A web tier runs in three AZs, with a total need of 300 instances. It must keep working at full capacity immediately if one AZ fails, with no dependency on launching new instances. What is the minimum number of instances it should run?

- A. 600, with 200 in each AZ
- B. 330, with 110 in each AZ
- C. 300, with 100 in each AZ
- D. 450, with 150 in each AZ

> [!success]- Answer
> **D.** If one AZ fails, the two remaining must carry 300, so each needs 150. That is 450 in total. 300 would leave 200 after a failure. 600 is more than needed.
>
> *Task 2.2.* Review: [[28 High Availability and Disaster Recovery#Removing single points of failure|Removing single points of failure]]

**12.** A company wants to convert CSV files in S3 to Parquet every night, with no servers to manage. What should a solutions architect use?

- A. Amazon Athena with a view
- B. AWS Direct Connect
- C. An EC2 instance with a cron job
- D. An AWS Glue ETL job on a schedule

> [!success]- Answer
> **D.** Glue is serverless ETL, and it can schedule jobs. EC2 needs management. A view does not change files.
>
> *Task 3.5.* Review: [[22 Data Lakes and Analytics#AWS Glue|AWS Glue]]

**13.** A company is redesigning an image service. Users upload files through an API, and processing can take up to 10 minutes. The service must keep accepting uploads during spikes, and it should cost almost nothing when idle. Which two design choices fit? (Choose two.)

- A. Run the API on an always-on EC2 instance with a local disk
- B. Send S3 events to an SQS queue, and process the queue with a Lambda function
- C. Process each image synchronously inside the API call
- D. Let clients upload directly to S3 with presigned URLs
- E. Hold uploads on instance store until they are processed

> [!success]- Answer
> **B and D.** Direct uploads remove your servers from the data path, and the queue buffers spikes while Lambda scales from zero. Synchronous processing ties up connections. An always-on instance costs money when idle. Instance store can lose data.
>
> *Task 2.1.* Review: [[07 S3 Security and Data Protection#Presigned URLs|Presigned URLs]]

**14.** A data pipeline runs as a Lambda function in Account A. It must read from a DynamoDB table in Account A and write the results to an S3 bucket in Account B. The objects must be owned by Account B. Which approach requires the least change to the function's permissions?

- A. Have the function assume a role in Account B for the whole run
- B. Replicate the DynamoDB table into Account B, and run the function there
- C. Create an IAM user in Account B, and store its access keys in the function's environment variables
- D. Add a bucket policy in Account B that allows the function's execution role to write objects, with the bucket's Object Ownership set to bucket owner enforced

> [!success]- Answer
> **D.** A resource policy lets the function keep its own permissions, so it can reach both the table and the bucket, and bucket owner enforced gives Account B ownership. Assuming a role gives up the Account A permissions. Replicating the table adds cost and complexity. Stored keys are the wrong pattern.
>
> *Task 1.1.* Review: [[02 IAM and Federation#Cross-account access|Cross-account access]]

**15.** A news site has users worldwide, and most content is images and HTML. Which service should be used to lower latency and load on the origin?

- A. Amazon CloudFront
- B. Amazon Route 53 weighted routing
- C. AWS Global Accelerator
- D. AWS Direct Connect

> [!success]- Answer
> **A.** CloudFront caches static content at the edge. Global Accelerator does not cache. Route 53 only answers DNS queries. Direct Connect links your data centre to AWS.
>
> *Task 2.1.* Review: [[12 CloudFront and Global Accelerator#Choosing between them|Choosing between them]]

**16.** An RDS database's storage use grows unpredictably, and an outage last year was caused by a full disk. What is the simplest prevention?

- A. Enable RDS Storage Auto Scaling with a maximum threshold
- B. Take more frequent snapshots
- C. Enable Multi-AZ
- D. Add a read replica

> [!success]- Answer
> **A.** Storage Auto Scaling grows storage automatically. Snapshots, replicas and Multi-AZ do not add free space.
>
> *Task 3.3.* Review: [[13 RDS and Aurora#Instance and storage|Instance and storage]]

**17.** A company imported a third-party TLS certificate into ACM for its ALB. Last month it expired, and caused an outage. How can the company get warning of this in future, with the least effort?

- A. Rely on ACM to renew the certificate automatically
- B. Use an EventBridge rule on ACM certificate expiry events, or the AWS Config `acm-certificate-expiration-check` rule, to notify the team
- C. Use CloudTrail to record the expiry
- D. Enable ALB access logs

> [!success]- Answer
> **B.** ACM sends expiry events for imported certificates, and Config has a managed rule. ACM does not renew imported certificates. CloudTrail and access logs do not warn in advance.
>
> *Task 1.3.* Review: [[23 Encryption and Secrets#Renewal|Renewal]]

**18.** A trading system must process orders for each account in the exact order received, with no duplicates, while orders for different accounts may be processed in parallel. Throughput is well below 300 messages per second. Which solution fits?

- A. An SNS standard topic with a Lambda subscriber
- B. An SQS FIFO queue, using the account ID as the message group ID
- C. Kinesis Data Streams with a random partition key
- D. An SQS standard queue with several workers

> [!success]- Answer
> **B.** Message groups keep order within an account, and FIFO removes duplicates. Standard queues have best-effort order. Standard SNS does not guarantee order. A random key breaks ordering.
>
> *Task 2.1.* Review: [[20 Messaging and Integration#FIFO queues|FIFO queues]]

**19.** A company wants to deliver clickstream data to S3 and Amazon OpenSearch Service in near real time, with Lambda transformation, and without writing consumers. What should it use?

- A. Amazon MQ
- B. AWS Batch
- C. Amazon SQS
- D. Amazon Data Firehose

> [!success]- Answer
> **D.** Firehose delivers to these destinations with no consumer code, and it can call Lambda. SQS needs consumers. Batch and MQ do not fit streaming delivery.
>
> *Task 3.5.* Review: [[21 Streaming and Data Ingestion#Amazon Data Firehose|Amazon Data Firehose]]

**20.** A company is moving users to a new Region gradually. It wants to send 10% of traffic there, and increase this over time. Which Route 53 policy fits?

- A. Simple routing
- B. Latency routing
- C. Failover routing
- D. Weighted routing

> [!success]- Answer
> **D.** Weights set the share of traffic that goes to each record. Latency depends on network conditions. Failover is active-passive. Simple cannot control shares.
>
> *Task 3.4.* Review: [[11 Route 53#Routing policies|Routing policies]]

**21.** An RDS database has an RPO of 15 minutes. Automated backups are enabled. Which statement is correct?

- A. Automated backups with transaction logs allow point-in-time restore to within about 5 minutes, so the RPO is met
- B. The RPO needs a read replica in another Region
- C. A daily snapshot alone meets the RPO
- D. The RPO needs Multi-AZ, because backups cannot meet it

> [!success]- Answer
> **A.** Transaction logs are backed up every 5 minutes, which meets a 15-minute RPO for restore. A daily snapshot alone gives an RPO of a day.
>
> *Task 4.3.* Review: [[28 High Availability and Disaster Recovery#Backup strategy|Backup strategy]]

**22.** A partner API must limit each partner to 100 requests per second and a monthly quota. The company must track usage per partner. What should a solutions architect use?

- A. A separate VPC for each partner
- B. WAF geo-match rules
- C. Lambda provisioned concurrency
- D. API Gateway usage plans with API keys

> [!success]- Answer
> **D.** Usage plans give per-client throttling and quotas. Geo-match acts on country. Provisioned concurrency is about cold starts. A VPC does not limit API calls.
>
> *Task 2.1.* Review: [[17 API Gateway and Front-End Services#Throttling and usage plans|Throttling and usage plans]]

**23.** A data lake uses SSE-KMS with millions of small objects, and KMS request charges are now a large part of the bill. Which change reduces them with the least effort?

- A. Add more prefixes
- B. Move to client-side encryption
- C. Enable S3 Bucket Keys on the bucket
- D. Disable encryption on the bucket

> [!success]- Answer
> **C.** Bucket Keys greatly reduce calls to KMS. Client-side encryption adds work. Encryption cannot be turned off for new objects. Prefixes do not change KMS calls.
>
> *Task 4.1.* Review: [[07 S3 Security and Data Protection#Encryption at rest|Encryption at rest]]

**24.** A company will run a fixed instance type in one AZ for three years, and it must guarantee capacity in that AZ. Which option gives the biggest discount and holds capacity?

- A. Regional Reserved Instances, No Upfront
- B. Spot Instances
- C. A Compute Savings Plan
- D. Zonal Standard Reserved Instances, All Upfront, for three years

> [!success]- Answer
> **D.** A zonal RI reserves capacity, and All Upfront for three years gives the best price. Savings Plans and Regional RIs do not hold capacity. Spot can be reclaimed.
>
> *Task 4.2.* Review: [[04 Amazon EC2#Reserved Instances|Reserved Instances]]

**25.** Which approach best balances cost and availability across workloads?

- A. Spot Instances for the production database
- B. Single-AZ for everything, including production
- C. Multi-AZ for production, and single-AZ with out-of-hours shutdown for development
- D. Multi-Region active-active for all workloads

> [!success]- Answer
> **C.** Spending on resilience should match each workload's needs. Multi-Region for everything is wasteful. Single-AZ production is a risk. Spot is wrong for a database.
>
> *Task 4.2.* Review: [[29 Cost Optimisation#Availability for each class of workload|Availability for each class of workload]]

**26.** An application behind an ALB must use HTTPS. The certificates must terminate at the load balancer, and the instances must not be reachable by anything except the ALB. Which two steps are needed? (Choose two.)

- A. Attach an ACM certificate to an HTTPS listener on the ALB
- B. Put the instances in a public subnet
- C. Install a certificate on each instance, and use a Gateway Load Balancer
- D. Attach an Elastic IP to each instance
- E. Allow inbound traffic to the instances only from the ALB's security group

> [!success]- Answer
> **A and E.** The listener terminates TLS, and the security group reference stops anyone going around the ALB. The other options expose instances or solve a different problem.
>
> *Task 1.2.* Review: [[05 Load Balancing and Auto Scaling#TLS on a load balancer|TLS on a load balancer]]

**27.** A team runs a read-heavy MySQL application with 12 read replicas, and it wants failover in under 30 seconds, storage that grows automatically, and replicas with very low lag. Which solution fits best?

- A. RDS for MySQL Multi-AZ instance deployment
- B. DynamoDB
- C. Amazon Aurora MySQL
- D. MySQL on EC2 with instance store

> [!success]- Answer
> **C.** Aurora shares storage across replicas, fails over quickly and grows automatically. RDS Multi-AZ takes longer, and its standby does not serve reads. EC2 means self-management. DynamoDB is not MySQL.
>
> *Task 2.2.* Review: [[13 RDS and Aurora#Amazon Aurora|Amazon Aurora]]

**28.** A news site reads the same articles from RDS many thousands of times per minute. Articles change rarely, and slightly stale data is acceptable for a few minutes. What is the most suitable design?

- A. Add a Multi-AZ standby
- B. Add ElastiCache with write-through and no TTL
- C. Add Amazon ElastiCache with lazy loading and a short TTL
- D. Move the database to a larger instance

> [!success]- Answer
> **C.** Lazy loading caches what is read, and a TTL limits staleness. Write-through helps when data must never be stale, and it caches items that are not read. Multi-AZ does not serve reads. A bigger instance is costlier and does less.
>
> *Task 2.1.* Review: [[15 ElastiCache and Other Databases#Caching strategies|Caching strategies]]

**29.** A company with one Direct Connect connection must reach VPCs in four Regions, in two accounts. Which component should it add?

- A. A virtual private gateway in one Region only
- B. An internet gateway in each VPC
- C. A Direct Connect gateway
- D. A LAG

> [!success]- Answer
> **C.** A Direct Connect gateway links a connection to VPCs across Regions and accounts. A LAG bundles links in one location. An internet gateway has nothing to do with Direct Connect.
>
> *Task 3.4.* Review: [[10 VPC Connectivity and Hybrid Networking#Direct Connect Gateway|Direct Connect Gateway]]

**30.** A company wants to move a Java application from on-premises servers into containers on AWS, keeping the option to run on other platforms. What is the correct order of the main steps?

- A. Deploy to ECS, then build the image, then create a registry
- B. Copy the JAR files to S3, then attach S3 as a Docker volume
- C. Create an AMI of the server, then run the AMI on Fargate
- D. Build a container image, push it to Amazon ECR, move state to managed services, and deploy on ECS or EKS

> [!success]- Answer
> **D.** The image comes first, then the registry, then externalising state, then deployment. S3 is not a Docker volume. Fargate runs container images, not AMIs.
>
> *Task 2.1.* Review: [[18 Containers#Moving an application into containers|Moving an application into containers]]

**31.** A company's policy says that encryption keys used by S3 must rotate every 180 days, and the rotation must be automatic. Which option meets this requirement?

- A. A customer managed KMS key with automatic rotation set to a 180-day period
- B. SSE-C with a key from the application
- C. An AWS managed key
- D. An AWS owned key

> [!success]- Answer
> **A.** Customer managed keys support custom automatic rotation periods. AWS managed keys rotate yearly, and you cannot change this. You cannot control AWS owned keys. SSE-C rotation would be entirely manual.
>
> *Task 1.3.* Review: [[23 Encryption and Secrets#Rotation|Rotation]]

**32.** A company runs a web application on EC2, a database on RDS, and static content in S3. Which two tasks does the company remain responsible for? (Choose two.)

- A. Patching the operating system on the EC2 instances
- B. Physical security of the data centres
- C. Patching the RDS database engine's host operating system
- D. Configuring access to the S3 bucket
- E. Replacing failed disks in the S3 service

> [!success]- Answer
> **A and D.** The customer owns the guest OS on EC2 and access configuration for its data. AWS patches the host OS under RDS, runs S3's hardware, and secures the facilities.
>
> *Task 1.1.* Review: [[01 Cloud Foundations#The shared responsibility model|The shared responsibility model]]

**33.** A company is moving to AWS and expects to create 100 accounts over two years. It wants a well-architected multi-account landing zone, central log archiving, standard account creation, and ongoing compliance reporting, with as little manual setup as possible. What should a solutions architect recommend?

- A. Create accounts by hand, and copy a CloudFormation template into each
- B. Set up AWS Control Tower, and use Account Factory for new accounts
- C. Use AWS Organizations with a single consolidated billing family
- D. Use one account with a VPC for each team

> [!success]- Answer
> **B.** Control Tower creates the landing zone and adds Account Factory and controls. Manual creation is slow and error-prone. Consolidated billing alone provides no governance. A single account gives poor isolation.
>
> *Task 1.1.* Review: [[03 Multi-Account Governance#AWS Control Tower|AWS Control Tower]]

**34.** A regulated company must keep a copy of all new S3 objects in a second Region, with a guarantee that 99.9% of objects are replicated within 15 minutes. What should a solutions architect configure?

- A. S3 Cross-Region Replication with Replication Time Control
- B. S3 Same-Region Replication
- C. S3 Batch Replication once an hour
- D. AWS Backup with a daily plan

> [!success]- Answer
> **A.** Replication Time Control adds a service level for replication time. Same-Region does not meet the second Region need. A daily backup is too slow. Batch Replication is for existing objects.
>
> *Task 1.3.* Review: [[06 Amazon S3#Replication|Replication]]

**35.** A company moves 20 TB per month from its data centre to AWS, and back, over a VPN. The transfer is slow and inconsistent. It wants lower data transfer cost and consistent speed. What should it use?

- A. AWS Global Accelerator
- B. AWS Direct Connect
- C. S3 Transfer Acceleration
- D. A second Site-to-Site VPN over the internet

> [!success]- Answer
> **B.** Direct Connect gives consistent bandwidth, and its data transfer out rate is lower than the internet. More VPNs still use the internet. The other two do not address this path.
>
> *Task 4.4.* Review: [[29 Cost Optimisation#Connection choices|Connection choices]]

**36.** A web application's business target is that 99.9% of requests succeed. Which CloudWatch metric best reflects that target for an ALB?

- A. Free disk space of the instances
- B. The rate of 5xx responses against total requests
- C. Average CPU of the instances
- D. Number of S3 buckets

> [!success]- Answer
> **B.** The error rate measures what users experience. CPU and disk space are indirect signals, and bucket count is unrelated.
>
> *Task 2.2.* Review: [[25 Monitoring and Auditing#Choosing metrics|Choosing metrics]]

**37.** A versioned bucket's storage bill keeps growing, because old versions pile up. Older versions are rarely needed after 30 days. What is the most effective step?

- A. Move current versions to Glacier
- B. Add a lifecycle rule to expire noncurrent versions after 30 days
- C. Delete the bucket's delete markers only
- D. Suspend versioning

> [!success]- Answer
> **B.** Noncurrent version expiration removes old versions. Suspending does not remove existing ones. Moving current versions affects live data.
>
> *Task 4.1.* Review: [[06 Amazon S3#Lifecycle rules|Lifecycle rules]]

**38.** A company's RDS instance is mostly busy serving repeated read queries. Which change could let it use a smaller instance?

- A. Enable storage autoscaling
- B. Add a cache such as Amazon ElastiCache
- C. Enable Multi-AZ
- D. Increase backup retention

> [!success]- Answer
> **B.** Caching removes repeated reads, so a smaller database can cope. The others do not reduce query load.
>
> *Task 4.3.* Review: [[29 Cost Optimisation#Database costs|Database costs]]

**39.** A company's DR plan relies on launching 500 instances in another Region during a disaster. What should it do to make sure this works?

- A. Request the needed service quota increases in the DR Region in advance, and test the plan
- B. Assume quotas are shared across Regions
- C. Use a larger instance type in the DR Region
- D. Request quota increases during the disaster

> [!success]- Answer
> **A.** Quotas are per Region, and they should be raised before they are needed. A request in the middle of a disaster may take too long.
>
> *Task 2.2.* Review: [[28 High Availability and Disaster Recovery#Quotas in a standby Region|Quotas in a standby Region]]

**40.** A compliance team must see the history of a security group's settings over the past six months, and must be told when any bucket allows public access. Which service meets both needs?

- A. Amazon Inspector
- B. AWS Config
- C. AWS X-Ray
- D. Amazon CloudWatch

> [!success]- Answer
> **B.** Config records configuration history and evaluates rules. CloudWatch shows performance. X-Ray traces requests. Inspector scans for vulnerabilities.
>
> *Task 1.3.* Review: [[25 Monitoring and Auditing#AWS Config|AWS Config]]

**41.** A REST API on API Gateway must accept tokens issued by a third-party identity provider, and the validation logic is custom. Which option should a solutions architect use?

- A. A Lambda authoriser
- B. An API key
- C. A resource policy based on IP addresses
- D. A Cognito user pool authoriser with no federation

> [!success]- Answer
> **A.** A Lambda authoriser runs custom logic to validate tokens. API keys identify clients and are not authentication. A user pool authoriser expects that pool's tokens. An IP policy does not validate tokens.
>
> *Task 1.2.* Review: [[17 API Gateway and Front-End Services#Security|Security]]

**42.** CloudWatch shows that many instances run at under 10% CPU. The team wants recommendations for smaller sizes, based on real usage. Which tool should it use?

- A. AWS Compute Optimizer
- B. Amazon Macie
- C. AWS Artifact
- D. AWS Budgets

> [!success]- Answer
> **A.** Compute Optimizer recommends sizes from usage history. Budgets track cost. Artifact gives compliance reports. Macie finds sensitive data.
>
> *Task 4.2.* Review: [[29 Cost Optimisation#AWS Compute Optimizer|AWS Compute Optimizer]]

**43.** A team runs an application on a provisioned DynamoDB table at a steady, predictable rate all day. Which capacity choice is likely to be cheapest?

- A. DAX with no other change
- B. A global table in three Regions
- C. Provisioned capacity with auto scaling
- D. On-demand capacity

> [!success]- Answer
> **C.** Predictable traffic suits provisioned capacity. On-demand suits unknown traffic. Global tables add replicas. DAX adds cost unless read latency is a problem.
>
> *Task 4.3.* Review: [[29 Cost Optimisation#Database costs|Database costs]]

**44.** Which two statements are true of storage durability and availability on AWS? (Choose two.)

- A. S3 One Zone-IA data is lost if its AZ is destroyed
- B. EBS volumes are replicated across Regions by default
- C. S3 Standard data is held in one AZ
- D. Instance store data survives an instance stop
- E. EBS volumes are replicated within a single AZ

> [!success]- Answer
> **A and E.** One Zone-IA uses one AZ, and EBS replicates within its AZ. EBS does not cross Regions by default. Instance store does not survive a stop. S3 Standard uses at least three AZs.
>
> *Task 2.2.* Review: [[08 Block and File Storage#Three kinds of storage|Three kinds of storage]]

**45.** A company wants on-premises applications to keep using NFS, with most data stored in S3, and recent files available locally with low latency. Which solution fits?

- A. Tape Gateway
- B. Volume Gateway, stored mode
- C. S3 File Gateway
- D. AWS Transfer Family

> [!success]- Answer
> **C.** S3 File Gateway gives NFS or SMB access to S3 with a local cache. Volume Gateway is block storage over iSCSI. Tape Gateway is for backups. Transfer Family is for SFTP-style exchange.
>
> *Task 3.1.* Review: [[27 Migration and Data Transfer#AWS Storage Gateway|AWS Storage Gateway]]

**46.** A security team wants to make sure that S3 buckets and KMS keys in the organisation can never be reached by principals outside the organisation, even if a developer writes a permissive bucket policy. Which control should it use?

- A. A permission boundary on each developer's role
- B. An AWS Config rule that reports public buckets
- C. A resource control policy attached to the organisation's root
- D. A service control policy attached to the organisation's root

> [!success]- Answer
> **C.** An RCP sets a ceiling on resources for all callers, including outsiders. An SCP affects only principals in your organisation. A boundary limits a developer's own permissions, but does not limit what a bucket policy allows to others. Config only reports.
>
> *Task 1.1.* Review: [[03 Multi-Account Governance#Policy ceilings compared|Policy ceilings compared]]

**47.** A company wants to start a workflow whenever a new file lands in S3, or a Zendesk ticket is opened, with routing based on the event's content, and it wants to replay events if a bug is found. What should a solutions architect use?

- A. AWS Direct Connect with a public VIF
- B. Amazon EventBridge with content-based rules and an archive
- C. Amazon SQS long polling
- D. Amazon SNS with email subscribers

> [!success]- Answer
> **B.** EventBridge takes AWS and SaaS events, routes on content, and can archive and replay. SQS and SNS do not integrate SaaS sources in this way, and they have no such replay.
>
> *Task 2.1.* Review: [[20 Messaging and Integration#Amazon EventBridge|Amazon EventBridge]]

**48.** A developer in a member account has an identity policy that allows `s3:*` on all resources. The account's SCP allows only `ec2:*`. The bucket in the same account has no bucket policy. What happens when the developer calls `s3:GetObject`?

- A. The request succeeds, because the identity policy allows it
- B. The request is denied, because the SCP does not allow the action
- C. The request is denied, because S3 needs a bucket policy for all access
- D. The request succeeds, because the bucket has no policy

> [!success]- Answer
> **B.** An SCP sets the maximum permissions, so an action outside it is denied even if IAM allows it. S3 does not need a bucket policy for same-account access when IAM allows it and no other control blocks it.
>
> *Task 1.1.* Review: [[02 IAM and Federation#Policy evaluation logic|Policy evaluation logic]]

**49.** A company must use FIPS-validated hardware, dedicated to it alone. Its security officers must have exclusive control of the keys, with no access by AWS. What should it use?

- A. AWS KMS with customer managed keys in the default key store
- B. AWS CloudHSM
- C. AWS KMS with AWS managed keys
- D. SSE-S3

> [!success]- Answer
> **B.** CloudHSM is single-tenant, and only the customer controls the keys. KMS is a shared service, even though its HSMs are validated. SSE-S3 keys are managed by AWS.
>
> *Task 1.3.* Review: [[23 Encryption and Secrets#AWS CloudHSM|AWS CloudHSM]]

**50.** A company wants to stop people accidentally deleting objects in a bucket, and to require a one-time code to permanently delete any version. What should a solutions architect do? (Choose two.)

- A. Enable default encryption with SSE-KMS
- B. Enable S3 Requester Pays
- C. Enable MFA Delete, using the root user of the bucket owner
- D. Enable S3 Transfer Acceleration
- E. Enable versioning on the bucket

> [!success]- Answer
> **C and E.** Versioning keeps old versions, and MFA Delete demands a code to permanently delete. The other features do not protect against deletion.
>
> *Task 1.3.* Review: [[07 S3 Security and Data Protection#Protecting against deletion|Protecting against deletion]]

**51.** A mobile app must let users sign up, sign in with Google, and then upload photos directly to a private S3 prefix of their own. Which combination should a solutions architect use? (Choose two.)

- A. A Cognito identity pool that exchanges the token for temporary AWS credentials, with a policy variable limiting access to each user's prefix
- B. IAM users for each app user
- C. A Cognito user pool for sign-up and sign-in, with Google as an identity provider
- D. Access keys embedded in the app, and encrypted with KMS
- E. IAM Identity Center for app users

> [!success]- Answer
> **A and C.** The user pool handles authentication, and the identity pool provides scoped temporary credentials. IAM users do not scale to app customers. Identity Center is for the workforce. Keys in an app can be extracted.
>
> *Task 1.1.* Review: [[02 IAM and Federation#Amazon Cognito|Amazon Cognito]]

**52.** A team's servers have drifted apart after years of manual patches, and deployments now fail unpredictably. What approach should a solutions architect recommend?

- A. Build new AMIs for each change, and replace instances through an Auto Scaling group instance refresh
- B. Move all configuration into a shared wiki
- C. Disable Auto Scaling, to keep the servers stable
- D. Keep patching servers by hand, with a detailed checklist

> [!success]- Answer
> **A.** Replacing instances from a known image prevents drift, and makes deployments repeatable. Manual patching is what caused the problem.
>
> *Task 2.2.* Review: [[26 Infrastructure as Code and Operations#Immutable infrastructure|Immutable infrastructure]]

**53.** A sales team wants Salesforce data copied into S3 every night, for analysis. The company does not want to write or host integration code. What should it use?

- A. AWS DataSync
- B. AWS Transfer Family
- C. Amazon AppFlow
- D. Amazon Kinesis Data Streams

> [!success]- Answer
> **C.** AppFlow connects SaaS applications to AWS with no code. Kinesis is for streaming with producers you run. DataSync moves storage, not SaaS data. Transfer Family handles SFTP and similar protocols.
>
> *Task 2.1.* Review: [[20 Messaging and Integration#Other integration services|Other integration services]]

**54.** A company hosts several customer sites on one fleet. Requests must be routed by hostname, and each site has its own TLS certificate. Which solution fits with the least infrastructure?

- A. One NLB for each customer
- B. One ALB with host-based listener rules and multiple certificates through SNI
- C. A Gateway Load Balancer
- D. A separate VPC for each customer

> [!success]- Answer
> **B.** ALB host-based routing and SNI serve many domains. An NLB per customer adds cost. A GWLB is for appliances. A VPC per customer is not needed.
>
> *Task 3.4.* Review: [[05 Load Balancing and Auto Scaling#Application Load Balancer|Application Load Balancer]]

**55.** Before removing an old role, the team wants to know which services the role has actually used in the last 90 days. Which tool gives this quickly?

- A. Amazon Inspector
- B. IAM credential report
- C. IAM last accessed data, shown in Access Advisor
- D. AWS Trusted Advisor

> [!success]- Answer
> **C.** Access Advisor shows when an identity last used each service. The credential report covers users and credential status. Trusted Advisor gives general checks. Inspector scans for vulnerabilities.
>
> *Task 1.1.* Review: [[02 IAM and Federation#Auditing IAM|Auditing IAM]]

**56.** A company runs an in-memory analytics engine that needs a lot of RAM, and low cost per GB of memory. Which instance family is most appropriate?

- A. C family
- B. I family
- C. T family
- D. R family

> [!success]- Answer
> **D.** R instances are memory optimised. C is compute optimised, T is burstable, and I is storage optimised.
>
> *Task 3.2.* Review: [[04 Amazon EC2#Instance types|Instance types]]

**57.** An application downloads parts of large S3 objects, and it wants to speed up transfers and recover from failed connections by retrying only the failed part. What should it use?

- A. S3 Replication
- B. S3 Select
- C. Multipart upload
- D. Byte-range fetches

> [!success]- Answer
> **D.** Byte-range requests fetch parts in parallel. S3 Select is closed to new customers, and it filters content by SQL. Replication copies objects. Multipart upload is for uploads.
>
> *Task 3.1.* Review: [[06 Amazon S3#Performance|Performance]]

**58.** Thousands of independent rendering jobs must run overnight. Each takes about an hour, and can be retried. The company wants managed scheduling, automatic scaling and low cost. Which is the best choice?

- A. AWS Lambda
- B. Amazon API Gateway
- C. AWS Batch using Spot Instances
- D. A single large On-Demand instance

> [!success]- Answer
> **C.** Batch manages queues and capacity, and Spot suits retryable jobs. Lambda stops at 15 minutes. One instance limits parallelism.
>
> *Task 3.2.* Review: [[19 Other Compute Services#AWS Batch|AWS Batch]]

**59.** A company transfers 40 TB per month between EC2 instances in two AZs. The application tolerates single-AZ operation. What is the most cost-effective change?

- A. Add a load balancer between them
- B. Move the instances into one AZ, and use private IP addresses
- C. Add a NAT gateway between them
- D. Use public IP addresses between the instances

> [!success]- Answer
> **B.** Same-AZ traffic over private IPs is generally free. Public addresses or added gateways increase cost.
>
> *Task 4.4.* Review: [[29 Cost Optimisation#Network costs|Network costs]]

**60.** A global game stores player profiles and needs low-latency reads and writes in three Regions. A short delay in replication is acceptable. Which solution fits?

- A. ElastiCache with a single primary
- B. DynamoDB global tables
- C. Aurora Global Database
- D. RDS read replicas in each Region

> [!success]- Answer
> **B.** Global tables are multi-active, so writes work in every Region. Aurora Global has one writer Region. Read replicas do not take writes.
>
> *Task 2.2.* Review: [[14 DynamoDB#Global tables|Global tables]]

**61.** A company has a data lake in S3, queried with Athena. Analysts in one department must see only certain columns of a sensitive table, and only rows for their region. What is the most effective way to achieve this?

- A. Create separate S3 buckets for each column
- B. Use IAM policies on the Glue crawler
- C. Use S3 bucket policies with conditions on column names
- D. Use AWS Lake Formation permissions for column and row filtering

> [!success]- Answer
> **D.** Lake Formation provides fine-grained, centralised permissions. S3 policies work at object level, and do not understand columns. A crawler is not an access control.
>
> *Task 1.3.* Review: [[22 Data Lakes and Analytics#Securing a data lake|Securing a data lake]]

**62.** The security team wants to be alerted automatically when an EC2 instance communicates with known malicious IP addresses or starts mining cryptocurrency. It wants no agents on instances. What should a solutions architect do?

- A. Run Amazon Inspector scans each week
- B. Enable Amazon Macie on all S3 buckets
- C. Install the CloudWatch agent, and create alarms on CPU
- D. Enable Amazon GuardDuty, and send findings through Amazon EventBridge to an SNS topic

> [!success]- Answer
> **D.** GuardDuty analyses logs with no agents, and it reports these threats. CPU alarms do not identify the cause. Macie finds sensitive data in S3. Inspector looks for software vulnerabilities.
>
> *Task 1.2.* Review: [[24 Threat Protection and Security Services#Amazon GuardDuty|Amazon GuardDuty]]

**63.** A company must inspect all outbound traffic from several VPCs, allow only an approved list of domains, and use stateful rules. It wants a managed service. What should a solutions architect recommend?

- A. Security groups on each instance with domain names
- B. AWS WAF on each ALB
- C. AWS Network Firewall in an inspection VPC, with routing through Transit Gateway
- D. Network ACLs with domain rules

> [!success]- Answer
> **C.** Network Firewall provides stateful inspection and domain filtering. Security groups and NACLs work with IP addresses, not domains. WAF protects web applications from inbound requests.
>
> *Task 1.2.* Review: [[09 VPC Fundamentals#AWS Network Firewall|AWS Network Firewall]]

**64.** A company must keep costs at a minimum for a non-critical system. An RTO of 24 hours and an RPO of 12 hours are acceptable. Which DR strategy is the best fit?

- A. Pilot light
- B. Multi-site active-active
- C. Warm standby
- D. Backup and restore

> [!success]- Answer
> **D.** Backup and restore is the cheapest strategy that meets these relaxed targets. The others run more resources all the time.
>
> *Task 2.2.* Review: [[28 High Availability and Disaster Recovery#Disaster recovery strategies|Disaster recovery strategies]]

**65.** Compliance requires monthly backups to be kept for 10 years. Monthly restores are rare. Which is the most cost-effective option for EC2 and RDS backups?

- A. Use automated RDS backups for 10 years
- B. Keep daily copies on instance store
- C. AWS Backup with a lifecycle rule that moves backups to cold storage where supported
- D. Keep all backups in warm storage for 10 years

> [!success]- Answer
> **C.** Lifecycle rules move rarely used backups to cheaper storage. Warm storage costs more. Instance store is temporary. Automated RDS backups stop at 35 days.
>
> *Task 4.1.* Review: [[28 High Availability and Disaster Recovery#Backup strategy|Backup strategy]]

## Score your exam

Mark your answers with the key, then count your correct answers for each domain.

> [!example]- Answer key
> 1: D · 2: D · 3: C · 4: A · 5: C · 6: B · 7: C · 8: D · 9: C · 10: B  
> 11: D · 12: D · 13: B, D · 14: D · 15: A · 16: A · 17: B · 18: B · 19: D · 20: D  
> 21: A · 22: D · 23: C · 24: D · 25: C · 26: A, E · 27: C · 28: C · 29: C · 30: D  
> 31: A · 32: A, D · 33: B · 34: A · 35: B · 36: B · 37: B · 38: B · 39: A · 40: B  
> 41: A · 42: A · 43: C · 44: A, E · 45: C · 46: C · 47: B · 48: B · 49: B · 50: C, E  
> 51: A, C · 52: A · 53: C · 54: B · 55: C · 56: D · 57: D · 58: C · 59: B · 60: B  
> 61: D · 62: D · 63: C · 64: D · 65: C  

| Domain | Questions | Your score |
| --- | --- | --- |
| Domain 1: Secure | 9, 10, 14, 17, 26, 31, 32, 33, 34, 40, 41, 46, 48, 49, 50, 51, 55, 61, 62, 63 | ___ / 20 |
| Domain 2: Resilient | 3, 11, 13, 15, 18, 22, 27, 28, 30, 36, 39, 44, 47, 52, 53, 60, 64 | ___ / 17 |
| Domain 3: High-Performing | 2, 4, 5, 6, 7, 12, 16, 19, 20, 29, 45, 54, 56, 57, 58 | ___ / 15 |
| Domain 4: Cost-Optimized | 1, 8, 21, 23, 24, 25, 35, 37, 38, 42, 43, 59, 65 | ___ / 13 |
| **Total** | | **___ / 65** |

Add your result to the table in the [[Study Guide#Tracking your progress|Study Guide]], and every mistake to the [[Mistake Log]].

---
**Previous:** [[Practice Exam 1]] · **Next:** [[Practice Exam 3]] · **Plan:** [[Study Guide]]
