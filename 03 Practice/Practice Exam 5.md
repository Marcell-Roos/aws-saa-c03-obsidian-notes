---
tags: [practice, scope/in]
---

# Practice Exam 5

> [!info] How to sit this exam
> - Set a timer for **130 minutes**, and sit it in one go, with no notes.
> - Write your answers on paper or in another note, and do not open the answers until you finish.
> - There are 65 questions. The real exam has 15 unscored questions, but all of these count here.
> - Score it with the table at the end, then review every question.
> - Aim for **75% or more** (49 of 65). See the [[Study Guide#Step 12 The readiness gate|readiness gate]].
>
> **This is the hardest exam in the vault.** Sit it last. Stems are longer, at least two options could usually work, and one stated requirement decides. A lower score than on the other exams is normal.
>
> These are original practice questions written for this vault. They are not real exam questions, their difficulty has not been calibrated against the real exam, and real questions are often longer, so expect to do more reading on the day.

**1.** A thumbnail service must process large TIFF files. Each file takes up to 12 minutes, and needs about 20 GB of memory. Files arrive unpredictably, and there may be none for hours. The company wants to pay nothing when idle and to have no servers to manage. Which option is the best fit?

- A. Use Lambda with reserved concurrency
- B. Use an EC2 Auto Scaling group with a minimum of 2 instances
- C. Start an ECS task on AWS Fargate for each file, using an EventBridge rule
- D. Use AWS Lambda with the maximum memory setting

> [!success]- Answer
> **C.** Fargate allows more memory than Lambda's limit of about 10 GB, and tasks run only when needed. Lambda's time limit would be fine, but its memory is not. An always-on group costs money when idle.
>
> *Task 2.1.* Review: [[16 Lambda and Serverless#Limits|Limits]]

**2.** A DynamoDB table holds 40 TB, most of which is years old and rarely read. Storage is now the largest part of the bill. Old data must stay in the table for simple queries. What is the most cost-effective change?

- A. Add a GSI on the date attribute
- B. Switch to provisioned capacity
- C. Change the table to the Standard-IA table class
- D. Enable DynamoDB Streams

> [!success]- Answer
> **C.** Standard-IA lowers storage cost for tables that are mostly stored data. A GSI adds cost. The capacity mode does not change storage. Streams add nothing here.
>
> *Task 4.3.* Review: [[14 DynamoDB#Capacity modes|Capacity modes]]

**3.** A content management system on Linux stores files on Amazon EFS in its primary Region. For disaster recovery, the company needs a copy of these files in another Region, with an RPO of under an hour. The operations team is small, and it wants the least work to set up and run this. What should a solutions architect use?

- A. A script that copies files with `rsync` from an EC2 instance
- B. AWS Backup with a weekly copy to the other Region
- C. EFS Replication to a file system in the DR Region
- D. AWS DataSync on a daily schedule

> [!success]- Answer
> **C.** EFS Replication runs continuously with an RPO of minutes. A daily or weekly copy misses the RPO. A script adds maintenance.
>
> *Task 2.2.* Review: [[28 High Availability and Disaster Recovery#Building blocks for each layer|Building blocks for each layer]]

**4.** A Lambda function must query an RDS database in a private subnet, and it must also call a public third-party tax API. The security team forbids public IP addresses on anything other than NAT devices, and the third party does not offer any private connectivity. Which design meets these requirements?

- A. Leave the function outside the VPC, and make the database public
- B. Attach the function to a public subnet with a route to an internet gateway
- C. Create an AWS PrivateLink connection to the third-party API
- D. Attach the function to private subnets that have a route to a NAT gateway in a public subnet

> [!success]- Answer
> **D.** Private subnets reach the database, and the NAT gateway reaches the internet. A function in a public subnet gets no public IP, so it has no internet access. A public database breaks the rule. PrivateLink needs the third party to offer an endpoint service.
>
> *Task 1.2.* Review: [[16 Lambda and Serverless#Lambda in a VPC|Lambda in a VPC]]

**5.** An application uses ElastiCache as a session store. When a primary node failed, it took a long time for a person to repair it, and users were logged out. The company wants automatic recovery within an AZ failure. What should it configure?

- A. Memcached with more nodes
- B. Append-only file persistence on a single node
- C. Multi-AZ with automatic failover, and a replica in another AZ
- D. Daily backups to S3

> [!success]- Answer
> **C.** Multi-AZ failover promotes a replica automatically. AOF does not protect against hardware or AZ failure. Memcached has no replication. Backups take time to restore.
>
> *Task 2.2.* Review: [[15 ElastiCache and Other Databases#High availability|High availability]]

**6.** A company is moving a Windows web application to AWS, and it cannot change the code. The application reads and writes shared files through an SMB path, and it uses a SQL Server database. The new design must survive the failure of one AZ with no data loss and no manual steps. Which design meets these requirements?

- A. EC2 instances across two AZs, FSx for Windows File Server Multi-AZ, and a SQL Server read replica
- B. One large EC2 instance with an io2 volume, with SQL Server on the same instance
- C. EC2 instances in an Auto Scaling group across two AZs behind an ALB, FSx for Windows File Server Multi-AZ, and RDS for SQL Server Multi-AZ
- D. EC2 instances across two AZs, Amazon EFS for the shared files, and RDS for SQL Server Multi-AZ

> [!success]- Answer
> **C.** FSx provides SMB with Multi-AZ failover, and RDS Multi-AZ fails over automatically with no data loss. EFS does not support Windows. One instance is a single point of failure. A read replica is asynchronous, and it needs manual promotion.
>
> *Task 2.2.* Review: [[28 High Availability and Disaster Recovery#Making legacy applications more reliable|Making legacy applications more reliable]]

**7.** A database serves a catalogue where product details change a few times a day. Reads are heavy. The company can accept data that is up to 5 minutes old, and cache memory is expensive, so only frequently read items should be cached. Which caching approach fits best?

- A. Lazy loading with a 5-minute TTL
- B. Write-through with no TTL
- C. Read replicas with no cache
- D. Write-through for all products, loaded at start-up

> [!success]- Answer
> **A.** Lazy loading caches only what is read, and the TTL limits staleness. Write-through caches everything, which wastes memory. Replicas still run a query for each read.
>
> *Task 3.3.* Review: [[15 ElastiCache and Other Databases#Caching strategies|Caching strategies]]

**8.** A research group has 100 TB of input data in S3, and runs a 3-day simulation each quarter. It needs a very fast shared POSIX file system. Results are written back to S3, so a failure can be handled by rerunning. It wants the lowest cost. Which option fits?

- A. FSx for Lustre with a Scratch deployment, linked to the bucket
- B. Amazon EFS with Provisioned throughput
- C. FSx for Lustre with a Persistent deployment, kept all year
- D. EBS volumes with Multi-Attach

> [!success]- Answer
> **A.** Scratch suits short-term, cheaper processing, and data is safe in S3. Persistent is for long-term use. EFS will not match this performance. Multi-Attach is limited to one AZ and 16 instances.
>
> *Task 3.1.* Review: [[08 Block and File Storage#FSx for Lustre|FSx for Lustre]]

**9.** A retailer wants clickstream events from its website stored in S3 as Parquet, for use by Athena. A delay of about 15 minutes is acceptable, and volumes vary widely through the day. The analytics team is small, and it wants no servers to manage and no custom consumer code to write. Which solution fits best?

- A. AWS Glue crawlers reading from the producers
- B. Amazon SQS with a Lambda function that appends to objects
- C. Kinesis Data Streams with a custom consumer on EC2 that writes Parquet
- D. Amazon Data Firehose with record format conversion, using a Glue table for the schema

> [!success]- Answer
> **D.** Firehose converts formats and delivers to S3 with no consumers. A custom consumer is more work. S3 objects cannot be appended to. A crawler discovers schemas, and it does not ingest streams.
>
> *Task 3.5.* Review: [[21 Streaming and Data Ingestion#Amazon Data Firehose|Amazon Data Firehose]]

**10.** A company has 150 accounts in AWS Organizations, grouped into OUs. Application teams have broad permissions in their own accounts, and they use a mix of IAM Identity Center roles and automation roles. A new policy says that only the shared networking account may create or attach internet gateways. The rule must apply immediately to current and future application accounts, and it must stop the action from happening, not just report it. Which solution meets these requirements with the least operational overhead?

- A. Remove the actions from every permission set in IAM Identity Center
- B. Use AWS Firewall Manager to apply a security group policy to all accounts
- C. Keep the networking account in its own OU, and attach an SCP to the application OUs that denies `ec2:CreateInternetGateway` and `ec2:AttachInternetGateway`
- D. Create an AWS Config rule that detects internet gateways, with an SSM Automation remediation that deletes them

> [!success]- Answer
> **C.** An SCP prevents the action for all principals in those accounts, and new accounts inherit it from the OU. A Config rule reacts after the gateway exists, so there is a window of exposure. Changing permission sets misses automation roles. Firewall Manager security group policies do not control internet gateways.
>
> *Task 1.1.* Review: [[03 Multi-Account Governance#Service control policies|Service control policies]]

**11.** A retailer's pricing service publishes price updates that three separate services must consume: the web shop, the mobile back end and the warehouse system. Each service needs every update for a product in order, and duplicates cause errors. The warehouse system is sometimes offline for maintenance, and it must be able to catch up at its own speed. Which design fits?

- A. Kinesis Data Firehose delivering to three buckets
- B. An SNS FIFO topic with an SQS FIFO queue for each service
- C. An SNS standard topic with an SQS standard queue for each service
- D. One SQS FIFO queue read by all three services

> [!success]- Answer
> **B.** FIFO fan-out gives ordering and deduplication, with a queue for each consumer. Standard topics do not guarantee order. In one queue each message goes to one consumer. Firehose does not suit this.
>
> *Task 2.1.* Review: [[20 Messaging and Integration#Fan-out|Fan-out]]

**12.** A company keeps its sales data in an on-premises Oracle database, connected to AWS by Direct Connect. The analytics team wants changes to appear in the S3 data lake within minutes, so that dashboards stay current. The database team will not allow any change to the application, and the source database must stay in production. Which solution fits?

- A. AWS Snowball Edge each week
- B. AWS DMS with change data capture, and S3 as the target
- C. AWS Transfer Family
- D. AWS DataSync on a 15-minute schedule

> [!success]- Answer
> **B.** DMS reads changes from the database log continuously. DataSync moves files and would not capture database changes. Snowball is far too slow. Transfer Family is for file exchange.
>
> *Task 3.5.* Review: [[27 Migration and Data Transfer#AWS DMS|AWS DMS]]

**13.** An S3 bucket policy allows the CloudTrail service to write logs to a bucket. A security review points out that any trail in any AWS account could be pointed at this bucket, which allows outsiders to write files there. What should a solutions architect add to the policy?

- A. A condition on `aws:MultiFactorAuthPresent`
- B. A condition on `aws:SecureTransport`
- C. A condition on `aws:SourceArn` or `aws:SourceAccount` that matches the company's own trail
- D. A second statement that allows `s3:PutObject` to the root user

> [!success]- Answer
> **C.** Source conditions stop a service being used on behalf of another account, which is the confused deputy problem for services. TLS and MFA conditions do not limit which trail writes the logs. A further allow does nothing to restrict access.
>
> *Task 1.1.* Review: [[02 IAM and Federation#Useful condition keys|Useful condition keys]]

**14.** A service has a contract that says at least 6 healthy instances must be running at all times, including during the failure of one of its three AZs. Auto Scaling cannot be relied on during such an event, because launches may be delayed. How should the Auto Scaling group be configured?

- A. Minimum of 7 instances, spread across three AZs
- B. Minimum of 6 instances, spread evenly across three AZs
- C. Minimum of 6 instances in one AZ
- D. Minimum of 9 instances, spread evenly across three AZs

> [!success]- Answer
> **D.** With 3 instances per AZ, losing one AZ leaves 6. With 6 in total, an AZ failure leaves 4. Seven still leaves fewer than 6 in the worst case.
>
> *Task 2.2.* Review: [[28 High Availability and Disaster Recovery#Removing single points of failure|Removing single points of failure]]

**15.** A media company serves static images to users worldwide. The images never change once published, and they are served through AWS Global Accelerator in front of an Application Load Balancer and EC2 instances. Origin load and data transfer charges are both rising with traffic. Which change should reduce latency, origin load and data transfer cost?

- A. Move the images to EBS volumes
- B. Add a second accelerator
- C. Replace Global Accelerator with CloudFront, for the static images
- D. Add NAT gateways in each Region

> [!success]- Answer
> **C.** CloudFront caches at the edge, and Global Accelerator does not, so every request still reaches the origin. The other options add cost.
>
> *Task 4.4.* Review: [[12 CloudFront and Global Accelerator#Choosing between them|Choosing between them]]

**16.** Regional managers need one dashboard, and each must see only rows for their own region. The company wants this without building separate dashboards. Which option fits?

- A. Separate Athena workgroups for each manager
- B. A bucket policy with a condition on region
- C. Amazon Managed Grafana with one dashboard per manager
- D. Amazon Quick with row-level security

> [!success]- Answer
> **D.** Row-level security filters data per user in one dashboard. Workgroups separate queries, not rows in a dashboard. Bucket policies work on objects. Separate dashboards are what the company wants to avoid.
>
> *Task 3.5.* Review: [[22 Data Lakes and Analytics#Amazon Quick|Amazon Quick]]

**17.** A containerised service runs at a steady 80% utilisation, around the clock, on Fargate, for at least the next three years. The team has the skills to manage EC2. Finance wants the lowest compute cost. Which option is likely to be cheapest?

- A. ECS on EC2 instances with a three-year Savings Plan
- B. Lambda functions
- C. Spot Instances for all tasks
- D. Fargate with no commitment

> [!success]- Answer
> **A.** Well-used EC2 with a commitment is generally cheaper for steady workloads. Fargate is priced for convenience. Lambda suits spiky traffic. Spot can be interrupted, and this is a steady service.
>
> *Task 4.2.* Review: [[29 Cost Optimisation#Compute costs|Compute costs]]

**18.** A bank runs encrypted RDS databases in one account. To protect against a Region failure and a compromised account, it must keep copies of its backups in a separate DR account, in a different Region. The copies must be made on a schedule, and the operations team wants the least custom work. Which solution fits best?

- A. Write a Lambda function that shares and copies snapshots on a schedule
- B. Enable RDS Multi-AZ, and copy the standby's data
- C. Create a cross-Region read replica in the DR account
- D. Use AWS Backup with a plan that has cross-Region and cross-account copy rules, and use customer managed KMS keys

> [!success]- Answer
> **D.** AWS Backup automates copies across Regions and accounts. A Lambda function would work, but it is custom code to maintain. A read replica is not a backup, because a bad change replicates too. Multi-AZ stays in one Region.
>
> *Task 1.3.* Review: [[28 High Availability and Disaster Recovery#AWS Backup|AWS Backup]]

**19.** A payments application runs on EC2 across three AZs. Compliance rules say that traffic must stay encrypted all the way to the servers, and that the application itself must terminate TLS and check client certificates. The company needs a load balancer that spreads connections without decrypting anything. Which option fits?

- A. A Network Load Balancer with a TCP listener
- B. A Network Load Balancer with a TLS listener
- C. An Application Load Balancer with an HTTPS listener
- D. CloudFront with field-level encryption

> [!success]- Answer
> **A.** A TCP listener passes encrypted traffic straight through. An HTTPS listener and a TLS listener both terminate TLS on the load balancer.
>
> *Task 3.4.* Review: [[05 Load Balancing and Auto Scaling#TLS on a load balancer|TLS on a load balancer]]

**20.** A Lambda function behind an API receives a steady 800 requests per second, and each request takes 1.5 seconds. The account has the default concurrency quota. During a load test, many requests are throttled. What is the best explanation and fix?

- A. The function needs 1,200 concurrent environments, so request a quota increase, or make the function faster
- B. The function needs 800 concurrent environments, so add memory
- C. The function has a cold start, so use SnapStart
- D. The function is limited to 100 requests per second, so add a queue

> [!success]- Answer
> **A.** Concurrency is requests per second multiplied by duration, so 800 × 1.5 = 1,200, above the default of 1,000. Memory may speed the function up, but the first figure is wrong. SnapStart does not change the concurrency needed.
>
> *Task 3.2.* Review: [[16 Lambda and Serverless#Cold starts and concurrency|Cold starts and concurrency]]

**21.** A company has set up a Site-to-Site VPN from its office to a virtual private gateway, and the console shows both tunnels as up. On-premises servers still cannot ping EC2 instances in a private subnet. The instances can reach each other, and the on-premises firewall has been confirmed to allow the traffic. Which two changes are most likely to be needed? (Choose two.)

- A. Enable DNS hostnames on the VPC
- B. Enable route propagation from the virtual private gateway in the subnet's route table
- C. Add a NAT gateway to the private subnet
- D. Attach an internet gateway to the VPC
- E. Allow ICMP from the on-premises range in the instances' security group

> [!success]- Answer
> **B and E.** The VPC needs a route back to the on-premises range, and security groups must allow ICMP. An internet gateway or NAT gateway deals with internet traffic. DNS hostnames do not affect pings by IP address.
>
> *Task 1.2.* Review: [[10 VPC Connectivity and Hybrid Networking#AWS Site-to-Site VPN|AWS Site-to-Site VPN]]

**22.** An ECS service on Fargate needs a database password. The password is in AWS Secrets Manager. The team references the secret in the task definition, so that it appears as an environment variable. Tasks now fail to start, with an error saying that the secret could not be retrieved. The task role has `secretsmanager:GetSecretValue`. What is the most likely fix?

- A. Add the permission to the EC2 instance profile
- B. Add the permission to the ECS service-linked role
- C. Move the secret into the container image
- D. Add `secretsmanager:GetSecretValue`, and KMS decrypt if needed, to the task execution role

> [!success]- Answer
> **D.** Secrets in a task definition are fetched by ECS at start-up, using the execution role. The task role is for calls that the application makes once it is running. Fargate has no instance profile for you to change. A secret in an image is insecure. The service-linked role is managed by AWS.
>
> *Task 1.2.* Review: [[18 Containers#Passing secrets to tasks|Passing secrets to tasks]]

**23.** A software vendor runs a reporting service in its own AWS account. The service must write files to an S3 bucket in each of 400 customer accounts, using short-lived credentials. Customers must be able to revoke access at any time. The vendor must be protected from a situation where one customer configures another customer's bucket details in the vendor's portal and so receives that customer's data. What is the most secure approach?

- A. Have the vendor create a bucket in its own account, and replicate to each customer
- B. Have each customer create a role that trusts the vendor's account and requires a unique ExternalId that the vendor generates for that customer, and have the service assume the role
- C. Have each customer create an IAM user, and give the access keys to the vendor
- D. Have each customer add a bucket policy that allows the vendor's service role

> [!success]- Answer
> **B.** A role gives temporary credentials, customers can revoke it, and a vendor-generated ExternalId stops the confused deputy problem. A bucket policy would work for access, but it gives no protection against a mismatched customer configuration. IAM users mean long-term keys. Replication does not give customers control, and it adds cost.
>
> *Task 1.1.* Review: [[02 IAM and Federation#Cross-account access|Cross-account access]]

**24.** An application uses Aurora Global Database, with a DR Region. Its database credentials are in AWS Secrets Manager in the primary Region. During a test of a Region failure, the DR application could not start, because it could not read the secret. What is the most operationally efficient fix?

- A. Use a KMS Multi-Region key, and leave the secret where it is
- B. Replicate the secret to the DR Region with Secrets Manager
- C. Copy the password into an environment variable in the DR Region
- D. Store the secret in a Parameter Store standard parameter in both Regions by hand

> [!success]- Answer
> **B.** Replication keeps the secret current in the other Region. Manual copies drift, especially with rotation. A Multi-Region key helps with encryption, but it does not make the secret available in that Region.
>
> *Task 1.3.* Review: [[23 Encryption and Secrets#AWS Secrets Manager|AWS Secrets Manager]]

**25.** An RDS for PostgreSQL database uses Provisioned IOPS storage, set to 20,000 IOPS when it was launched three years ago. CloudWatch shows an average of 3,000 IOPS, with peaks of 8,000 at month-end. Its latency needs are ordinary, and the application does not justify paying for unused performance. What is the most cost-effective change?

- A. Add a read replica
- B. Move to magnetic storage
- C. Increase provisioned IOPS to 40,000
- D. Move to General Purpose SSD (gp3) storage, with IOPS set to meet the peaks

> [!success]- Answer
> **D.** gp3 can provide this level at a lower cost. More IOPS costs more. Magnetic storage is legacy, and it cannot meet the peaks. A replica adds an extra instance.
>
> *Task 4.3.* Review: [[13 RDS and Aurora#Instance and storage|Instance and storage]]

**26.** A company needs a 100 TB Windows file share for office documents. Most files are cold, throughput needs are low, and many documents are near-duplicates of each other. The share must integrate with Active Directory and survive an AZ failure, at the lowest cost. Which configuration fits?

- A. FSx for Lustre, with a Scratch deployment
- B. Amazon EFS with Infrequent Access
- C. FSx for Windows File Server, Multi-AZ, with HDD storage and data deduplication
- D. FSx for Windows File Server, Multi-AZ, with SSD storage

> [!success]- Answer
> **C.** HDD storage and deduplication lower the cost for general file shares. SSD costs more than these needs justify. EFS does not support Windows, and Lustre is for HPC.
>
> *Task 4.1.* Review: [[08 Block and File Storage#FSx for Windows File Server|FSx for Windows File Server]]

**27.** A bucket in Account A holds objects encrypted with SSE-KMS, using the AWS managed key `aws/s3`. A bucket policy allows a role in Account B to read them, and the role's IAM policy allows it too. Reads fail with `AccessDenied`. Plain objects in the same bucket can be read. What should a solutions architect do?

- A. Re-encrypt the objects with a customer managed key, and allow Account B in its key policy and in the role's IAM policy
- B. Enable S3 Versioning, and copy the objects
- C. Add Account B to the policy of the `aws/s3` key
- D. Turn off Block Public Access on the bucket

> [!success]- Answer
> **A.** The policy of an AWS managed key cannot be changed, so such keys cannot be used across accounts. A customer managed key can. Block Public Access and versioning have nothing to do with this error.
>
> *Task 1.3.* Review: [[07 S3 Security and Data Protection#Cross-account access to a bucket|Cross-account access to a bucket]]

**28.** A Java order service runs on `m5` instances in an Auto Scaling group. Traffic is steady, but the service has become slow. CloudWatch shows CPU at about 20%, and the CloudWatch agent shows memory at 97%, with heavy swapping. The team wants to fix the cause, and it does not want to redesign the application. Which change is the most appropriate?

- A. Enable T instance Unlimited mode
- B. Move to a memory-optimised R family instance of a suitable size
- C. Move to a compute-optimised C family instance
- D. Add more EBS IOPS

> [!success]- Answer
> **B.** The bottleneck is memory, so a memory-optimised family fits. A compute family has less memory per vCPU. More IOPS treats the symptom. T instances do not help here.
>
> *Task 3.2.* Review: [[04 Amazon EC2#Instance types|Instance types]]

**29.** A company runs an EKS cluster, and its security team requires a monitoring agent on every node. The agent runs as a Kubernetes DaemonSet in privileged mode. The company wants to reduce node management as far as possible. Which compute option should it use?

- A. EKS managed node groups
- B. Amazon ECS on Fargate
- C. AWS Fargate for all pods
- D. AWS Lambda

> [!success]- Answer
> **A.** Managed node groups reduce the work and allow DaemonSets. Fargate on EKS does not support DaemonSets or privileged containers. ECS and Lambda are not Kubernetes.
>
> *Task 2.1.* Review: [[18 Containers#Node types|Node types]]

**30.** A video-sharing startup lets users upload clips of up to 200 MB through a REST API on API Gateway, which invokes a Lambda function that writes each file to S3. Users report failed uploads, and the company pays for Lambda time while files pass through the function. Traffic is expected to grow tenfold this year. Which redesign best improves reliability and reduces cost?

- A. Enable API Gateway caching
- B. Increase the Lambda memory and timeout
- C. Use a WebSocket API for the uploads
- D. Have the API return a presigned S3 URL, and let the client upload directly to S3

> [!success]- Answer
> **D.** API Gateway limits payloads to 10 MB and Lambda to 6 MB synchronously, so large files should go directly to S3. Caching does not help uploads. More memory does not change payload limits.
>
> *Task 2.1.* Review: [[07 S3 Security and Data Protection#Presigned URLs|Presigned URLs]]

**31.** A company is building a delivery-tracking application. It needs a relational database with geospatial queries through the PostGIS extension, automatic failover in under a minute, and up to 15 read replicas with low lag. The development team has no preference for an engine, as long as these needs are met. Which option fits best?

- A. Amazon Aurora PostgreSQL-Compatible Edition
- B. Amazon Aurora MySQL-Compatible Edition
- C. Amazon DynamoDB
- D. Amazon Redshift

> [!success]- Answer
> **A.** PostGIS is a PostgreSQL extension, and Aurora adds replicas and failover. Aurora MySQL has no PostGIS. DynamoDB is not relational. Redshift is a data warehouse.
>
> *Task 3.3.* Review: [[13 RDS and Aurora#Amazon RDS|Amazon RDS]]

**32.** A company tested failover on its Aurora MySQL cluster. A replica was promoted correctly within 30 seconds, but the application kept failing to write until an engineer changed its configuration. Its connection string uses the DNS name of the original writer instance. The team wants failover to work with no manual step. What should a solutions architect recommend?

- A. Connect through the reader endpoint
- B. Add a second Aurora writer
- C. Add a Route 53 failover record for the instance endpoint
- D. Connect through the cluster (writer) endpoint

> [!success]- Answer
> **D.** The cluster endpoint always points at the current writer. The reader endpoint is for reads. A Route 53 record adds work that the cluster endpoint already does.
>
> *Task 2.2.* Review: [[13 RDS and Aurora#Endpoints|Endpoints]]

**33.** A company has 30 VPCs in one Region, all connected by a Transit Gateway. Each VPC has its own interface endpoints, across three AZs, for the same five AWS services. The security team requires that this traffic stays private, but the endpoints' hourly charges have become significant. What is the most cost-effective design?

- A. Create gateway endpoints for all five services
- B. Create the endpoints in one shared services VPC, and reach them through Transit Gateway with private hosted zones
- C. Remove the endpoints, and use the internet through NAT
- D. Create more endpoints in each AZ

> [!success]- Answer
> **B.** Sharing endpoints reduces the number of hourly charges. Gateway endpoints exist only for S3 and DynamoDB. NAT is often more expensive at volume, and it may break a private access requirement.
>
> *Task 4.4.* Review: [[10 VPC Connectivity and Hybrid Networking#VPC endpoints|VPC endpoints]]

**34.** A company keeps customer uploads in several general-use S3 buckets. A new data protection rule says that any object containing personal data must be moved to a restricted bucket as soon as it is found. The security team is small, and it does not want to write its own detection logic or run servers. Which solution has the least custom infrastructure?

- A. Use AWS Config, with a rule that reads each object
- B. Use Amazon GuardDuty, with an EventBridge rule that invokes a Lambda function
- C. Use Amazon Macie, with an EventBridge rule on findings that invokes a Lambda function to move the object
- D. Use a nightly EC2 script that searches all objects

> [!success]- Answer
> **C.** Macie finds personal data, and EventBridge connects its findings to a fix. GuardDuty looks for threats and not data types. Config does not read object contents. A custom script is a lot of work, and it is delayed.
>
> *Task 1.3.* Review: [[24 Threat Protection and Security Services#Automating a response|Automating a response]]

**35.** Workloads in private subnets across 12 VPCs must reach only an approved list of software repositories by domain name. All other outbound traffic must be blocked and logged, including attempts to connect directly to IP addresses. The security team wants a managed service and a single set of rules. What should a solutions architect recommend?

- A. Route outbound traffic through a central inspection VPC with AWS Network Firewall, using stateful domain allow-list rules
- B. Use security groups with outbound rules that list the repositories' domain names
- C. Use Route 53 Resolver DNS Firewall in each VPC to block all other domains
- D. Use AWS WAF on each NAT gateway

> [!success]- Answer
> **A.** Network Firewall inspects traffic itself, so it also stops direct connections to IP addresses, and it logs them. DNS Firewall only affects name lookups, so a direct connection to an IP gets through. Security groups do not accept domain names. WAF does not attach to NAT gateways.
>
> *Task 1.2.* Review: [[09 VPC Fundamentals#AWS Network Firewall|AWS Network Firewall]]

**36.** A company enabled Cross-Region Replication on a production bucket, with versioning on both buckets and a replication role in place. Some objects appear in the destination, but others do not. A check shows that objects encrypted with SSE-S3 are replicating, and objects encrypted with SSE-KMS are not. Which two steps are needed? (Choose two.)

- A. Enable replication of KMS-encrypted objects in the rule, and name a KMS key in the destination Region
- B. Give the replication role `kms:Decrypt` on the source key, and `kms:Encrypt` on the destination key
- C. Convert the objects to SSE-C
- D. Disable versioning on the destination bucket
- E. Enable S3 Transfer Acceleration on both buckets

> [!success]- Answer
> **A and B.** SSE-KMS replication is optional, and it needs a destination key and permissions on both keys. Versioning is required on both buckets. SSE-C is unnecessary, and Transfer Acceleration does not affect replication.
>
> *Task 1.3.* Review: [[06 Amazon S3#Replication|Replication]]

**37.** A bank's security policy says that all KMS keys must rotate at least yearly. Most keys are customer managed with automatic rotation. However, one key was created with imported key material, because a regulator requires the bank to generate the material itself, and the automatic rotation option cannot be enabled. What should the team do to meet the policy?

- A. Convert the key to an AWS managed key
- B. Delete the key, and encrypt the data with SSE-S3
- C. Open a support case to enable automatic rotation
- D. Rotate it on demand with new imported key material, or create a new key and move the alias

> [!success]- Answer
> **D.** Automatic rotation is not available for imported material, so rotation has to be done on demand, or manually by moving an alias to a new key. AWS Support cannot enable it. Keys cannot be converted. Deleting the key would make its data unreadable.
>
> *Task 1.3.* Review: [[23 Encryption and Secrets#Rotation|Rotation]]

**38.** A company has an internal REST API on API Gateway. Only applications in one specific VPC may call it, and traffic must not cross the internet. Applications in other VPCs in the same account must be refused, even if they have an interface endpoint of their own. Which configuration meets these requirements?

- A. Use an edge-optimised API with a Lambda authoriser that checks the source IP
- B. Use a private API with an API key for each VPC
- C. Use a Regional API with a WAF IP set that lists the VPC's NAT gateway address
- D. Use a private API, create an interface endpoint in the VPC, and add a resource policy that allows only requests with that `aws:SourceVpce`

> [!success]- Answer
> **D.** A private API stays off the internet, and the resource policy limits it to one endpoint. A Regional API with a WAF rule is still reached over a public endpoint. An edge-optimised API is public. API keys identify clients and do not restrict network paths.
>
> *Task 1.2.* Review: [[17 API Gateway and Front-End Services#Security|Security]]

**39.** A company must keep monthly EBS snapshots of a financial system for seven years, for compliance. Auditors have asked for a restore only once in ten years, and the team can wait up to three days when this happens. The snapshots are now a noticeable part of the storage bill. Which option is the most cost-effective?

- A. Keep each one as a running volume
- B. Move the snapshots to the EBS Snapshot Archive tier
- C. Keep them in the standard snapshot tier
- D. Enable Fast Snapshot Restore on all of them

> [!success]- Answer
> **B.** Archive is up to 75% cheaper for snapshots kept for a long time. Standard costs more. Volumes cost far more. Fast Snapshot Restore adds cost.
>
> *Task 4.1.* Review: [[08 Block and File Storage#Snapshots|Snapshots]]

**40.** A company wants to break a large web application on EC2 into microservices, one feature at a time. All traffic comes in through one domain. Clients must not change, and the old application must keep serving everything that has not yet moved. What is the best approach?

- A. Add listener rules on the existing Application Load Balancer that send paths for migrated features to new target groups
- B. Use Route 53 weighted routing to send feature paths to the new services
- C. Rewrite the entire application, and switch over in one release
- D. Replace the ALB with an NLB, and create a listener for each feature

> [!success]- Answer
> **A.** ALB path rules move features one at a time, and clients see no change. DNS does not see URL paths. An NLB cannot route on paths. A full rewrite is what the company wants to avoid.
>
> *Task 2.1.* Review: [[31 Architecture Patterns#Microservices|Microservices]]

**41.** A security team wants events from every account in its organisation to reach an event bus in a central security account, where rules trigger automated responses. The organisation adds several accounts each month, and the team does not want to update the central account each time. Which approach needs the least ongoing work?

- A. List every account ID in the bus's resource policy, and update it each month
- B. Add a resource-based policy to the central bus that allows `events:PutEvents` with a condition on `aws:PrincipalOrgID`, and deploy a forwarding rule to each account with CloudFormation StackSets
- C. Create an IAM user in the central account for each account to use
- D. Send all events to an SQS queue in each account, and poll the queues from the central account

> [!success]- Answer
> **B.** The condition covers new accounts automatically, and service-managed StackSets can deploy the rule to them. Listing accounts needs a change each month. IAM users mean long-term keys. Polling queues adds work and delay.
>
> *Task 1.1.* Review: [[02 IAM and Federation#Cross-account access|Cross-account access]]

**42.** A company runs an internal API on an API Gateway REST API, which uses only Lambda proxy integrations and JWT authorisation. It does not use API keys, caching, WAF or request validation. Bills are high, because the request volume is large and steady. Which change reduces cost, with the least effort?

- A. Move to an edge-optimised endpoint
- B. Move to an HTTP API
- C. Add a usage plan with a low quota
- D. Enable response caching for all routes

> [!success]- Answer
> **B.** HTTP APIs are much cheaper, and they support these features. Caching adds an hourly cost, and it does not suit all routes. Edge optimisation does not reduce API charges. A low quota would reject valid requests.
>
> *Task 4.2.* Review: [[17 API Gateway and Front-End Services#REST or HTTP API|REST or HTTP API]]

**43.** An EKS cluster has used nearly all the addresses in a VPC with a /22 CIDR, and new pods fail to start. The VPC is connected to other networks that use `10.0.0.0/8`. What should a solutions architect do with the least disruption?

- A. Add a secondary CIDR block from a range that does not overlap, and create new subnets for pods
- B. Use public IPv4 addresses for pods
- C. Change the existing subnets to a larger size
- D. Create a new VPC, and rebuild the cluster

> [!success]- Answer
> **A.** A VPC can have secondary CIDR blocks. Subnets cannot be resized. A rebuild is unnecessary disruption. Public addresses are not the answer for pods.
>
> *Task 3.4.* Review: [[09 VPC Fundamentals#IP addressing and CIDR|IP addressing and CIDR]]

**44.** A log analytics application on EC2 needs 12 TiB of block storage, with about 400 MiB/s of sequential reads throughout the day. IOPS are not important, and it must be the lowest-cost EBS option that meets this. Which volume type fits?

- A. sc1
- B. io2 Block Express
- C. st1
- D. gp3

> [!success]- Answer
> **C.** st1 is built for frequent sequential throughput, up to 500 MiB/s. sc1 stops at 250 MiB/s. SSD types would work, but they cost much more for this size.
>
> *Task 3.1.* Review: [[08 Block and File Storage#Volume types|Volume types]]

**45.** A dynamic HTTPS API runs in one Region and has users worldwide. The company wants lower latency, TLS termination close to users and WAF filtering at the edge. Responses cannot be cached. Static IPs are not needed. Which service fits best?

- A. Amazon CloudFront with caching disabled for the API
- B. AWS Global Accelerator
- C. Route 53 geolocation routing
- D. S3 Transfer Acceleration

> [!success]- Answer
> **A.** CloudFront terminates TLS at the edge, carries traffic over the AWS network and integrates with WAF, even when nothing is cached. Global Accelerator improves routing, but it does not terminate TLS at the edge or attach WAF. Route 53 only answers DNS queries.
>
> *Task 3.4.* Review: [[12 CloudFront and Global Accelerator#Choosing between them|Choosing between them]]

**46.** A storage team manages a bucket with several petabytes of mixed data in S3 Standard. It suspects that much of this data stops being read after a few weeks, but it does not know when, so it cannot set a lifecycle rule with confidence. It wants evidence of access patterns before moving anything. Which tool provides this directly?

- A. S3 Inventory
- B. S3 Storage Class Analysis
- C. AWS Budgets
- D. CloudTrail management events

> [!success]- Answer
> **B.** Storage Class Analysis watches access patterns and recommends when to transition. Inventory lists objects. Management events do not show object reads. Budgets track spending.
>
> *Task 4.1.* Review: [[06 Amazon S3#Tools for managing S3 at scale|Tools for managing S3 at scale]]

**47.** A company uses IAM Identity Center with Okta as its identity provider. Engineers belong to one of about 200 cost centres, and new ones appear each month. Engineers must be able to stop and start only EC2 instances tagged with their own cost centre. The security team wants to avoid changing policies when a cost centre is added. What should a solutions architect do?

- A. Create an IAM group in each account for each cost centre
- B. Create a permission set for each cost centre, with the instance ARNs listed in each one
- C. Create an SCP for each cost centre, and attach them to the accounts
- D. Enable attributes for access control, pass the cost centre from Okta, and use one permission set whose policy compares `aws:PrincipalTag/CostCenter` with `ec2:ResourceTag/CostCenter`

> [!success]- Answer
> **D.** ABAC needs one policy, and it keeps working as cost centres are added. A permission set or group per cost centre grows with each new one, and instance ARNs change. SCPs apply to accounts, and they cannot express per-user rules like this.
>
> *Task 1.1.* Review: [[02 IAM and Federation#Least privilege|Least privilege]]

**48.** A regulator requires encryption keys to stay in a company's own hardware security module in its data centre, outside AWS. The company still wants AWS services such as S3 and EBS to use those keys through normal KMS integration. Which solution meets this requirement?

- A. An AWS KMS external key store
- B. A KMS key with imported key material
- C. SSE-C with keys held by the application
- D. An AWS KMS custom key store backed by AWS CloudHSM

> [!success]- Answer
> **A.** An external key store keeps keys in your own key manager, and works through KMS. A CloudHSM key store holds keys inside AWS. Imported material still lives in KMS. SSE-C works for S3, but it does not provide KMS integration for other services.
>
> *Task 1.3.* Review: [[23 Encryption and Secrets#Custom key stores|Custom key stores]]

**49.** Fleet devices send 20 MB per second of telemetry. Each device's readings must be processed in order. Two separate applications read the data, and the team needs to reprocess the last 3 days after any failure. Which service is the best fit?

- A. SQS FIFO, with the device ID as the message group ID
- B. Kinesis Data Streams, with the device ID as the partition key
- C. Amazon SNS FIFO topic
- D. Amazon Data Firehose

> [!success]- Answer
> **B.** Kinesis supports many independent readers, ordering per key, and replay. In SQS, a message is removed once it is processed, so two applications cannot both read it and it cannot be replayed. A standard SNS topic does not hold messages for replay. Firehose delivers data and has no replay.
>
> *Task 2.1.* Review: [[21 Streaming and Data Ingestion#Ordering|Ordering]]

**50.** A Lambda function with a 5-minute timeout processes orders from an SQS standard queue. The queue has its default visibility timeout of 30 seconds. Customers have complained about being charged twice, and logs show that many messages are being processed more than once. The team wants to fix this without moving away from SQS and Lambda. Which combination fixes this? (Choose two.)

- A. Use reserved concurrency of 1
- B. Change to long polling of 20 seconds
- C. Raise the queue's visibility timeout to at least six times the function timeout
- D. Lower the queue's retention period
- E. Make the order processing idempotent

> [!success]- Answer
> **C and E.** Messages reappear while still being processed, so the timeout must be longer. Standard queues can still deliver a message twice, so consumers should be idempotent. Long polling reduces empty receives. Limiting concurrency slows processing, and it does not stop reappearing messages.
>
> *Task 2.1.* Review: [[16 Lambda and Serverless#Event source mappings in detail|Event source mappings in detail]]

**51.** A company's analysts run reports for about two hours a day, at unpredictable times. The reports run on a provisioned Amazon Redshift cluster that stays on all day, and it sits idle for most of that time. The finance team has asked for lower costs, and the data team does not want to manage pausing or resizing clusters. Which change reduces cost with the least administration?

- A. Move to Amazon Redshift Serverless
- B. Move the data to DynamoDB
- C. Buy Reserved Instances for the cluster
- D. Add Concurrency Scaling

> [!success]- Answer
> **A.** Serverless charges for what is used, so idle time is free. Reserved Instances commit to always-on capacity. Concurrency Scaling adds capacity. DynamoDB is not for analytics.
>
> *Task 4.3.* Review: [[22 Data Lakes and Analytics#Amazon Redshift|Amazon Redshift]]

**52.** An application runs on EC2 behind an Application Load Balancer. Customers must sign in with an email address, or with Google, before reaching any page. The company wants to manage users in AWS, and it cannot change the application's code. Which solution fits best?

- A. Use IAM Identity Center with Google as the identity source
- B. Create a Cognito user pool with Google as an identity provider, and add an authenticate-cognito action to the ALB listener rule
- C. Put API Gateway in front of the ALB with a Cognito authoriser, and rewrite the routes
- D. Use a Lambda@Edge function that implements OAuth on a new CloudFront distribution

> [!success]- Answer
> **B.** ALB can authenticate users through a Cognito user pool, with no code changes. API Gateway adds another layer and more change. Identity Center is for the workforce. A custom Lambda@Edge login is much more work.
>
> *Task 1.2.* Review: [[05 Load Balancing and Auto Scaling#Application Load Balancer|Application Load Balancer]]

**53.** An application runs in two Regions. Each Region must read and write S3 data in its own Region, using a single global name. If a Region has problems, requests should go to the other, and data written in either Region must appear in both. Which two features should be used? (Choose two.)

- A. S3 Transfer Acceleration
- B. Two-way S3 replication between the buckets
- C. One-way replication to a backup bucket
- D. CloudFront with an origin group
- E. S3 Multi-Region Access Point

> [!success]- Answer
> **B and E.** A Multi-Region Access Point gives one global endpoint with routing, and two-way replication keeps both buckets current. Origin groups only fail over reads. Transfer Acceleration does not provide failover. One-way replication leaves a Region without the other's writes.
>
> *Task 2.2.* Review: [[06 Amazon S3#Other features|Other features]]

**54.** A company runs a TCP game service behind a Network Load Balancer, and players connect to fixed IP addresses. After a large attack, the company wants 24/7 access to DDoS specialists, and credit for scaling costs caused by attacks. What should a solutions architect recommend?

- A. Attach AWS WAF to the NLB, with a rate-based rule
- B. Rely on AWS Shield Standard, and raise the Auto Scaling maximum
- C. Assign Elastic IPs to the NLB, subscribe to AWS Shield Advanced, and protect those Elastic IPs
- D. Use Amazon GuardDuty with an automated response

> [!success]- Answer
> **C.** Shield Advanced adds the response team and cost protection, and it protects Elastic IPs. WAF does not attach to an NLB. Shield Standard offers neither benefit. GuardDuty detects threats, and it does not mitigate DDoS attacks.
>
> *Task 1.2.* Review: [[24 Threat Protection and Security Services#AWS Shield|AWS Shield]]

**55.** A retailer is moving a product table to DynamoDB, using provisioned capacity. Items are a consistent 3.5 KB. At peak, the application makes 1,000 standard writes per second and 2,000 eventually consistent reads per second, with no transactions. The finance team wants the table sized for that peak, with no spare capacity. What capacity should be provisioned?

- A. 3,500 WCU and 2,000 RCU
- B. 4,000 WCU and 2,000 RCU
- C. 1,000 WCU and 2,000 RCU
- D. 4,000 WCU and 1,000 RCU

> [!success]- Answer
> **D.** Writes round up to 4 KB, which is 4 WCU each, so 4,000 WCU. Reads round up to 4 KB, which is 0.5 RCU each when eventually consistent, so 1,000 RCU.
>
> *Task 3.3.* Review: [[14 DynamoDB#Calculating capacity|Calculating capacity]]

**56.** An online store's dashboards show healthy CPU, memory and latency across all tiers. Even so, a bug in a recent release stopped checkouts for an hour, and nobody noticed until customers complained. The business wants to be alerted when completed orders fall below the normal rate. What should a solutions architect recommend?

- A. Use AWS Trusted Advisor
- B. Publish a custom CloudWatch metric for completed orders, and create an alarm on it
- C. Enable AWS CloudTrail Insights
- D. Create a CloudWatch alarm on average CPU

> [!success]- Answer
> **B.** A business metric shows what matters to customers. CPU looks normal here. CloudTrail Insights looks at API activity. Trusted Advisor gives best-practice checks.
>
> *Task 2.2.* Review: [[25 Monitoring and Auditing#Choosing metrics|Choosing metrics]]

**57.** Twenty internal consumers need different subsets of order events, chosen on fields deep inside each JSON event. After a recent bug, the team also wants to be able to reprocess last week's events. Which service meets both requirements with the least operational overhead?

- A. Amazon SNS standard topic with subscription filter policies
- B. Amazon Kinesis Data Streams with a custom consumer for each team
- C. Amazon SQS with a queue for each consumer, and a Lambda router
- D. Amazon EventBridge, with content-based rules and an archive

> [!success]- Answer
> **D.** EventBridge filters on content, and it can archive and replay. SNS can filter, but a standard topic cannot replay. Kinesis can replay, but each team would need to write filtering consumers. A Lambda router is custom code.
>
> *Task 2.1.* Review: [[20 Messaging and Integration#Amazon EventBridge|Amazon EventBridge]]

**58.** An audit finds that an Amazon EFS file system holding customer data was created two years ago without encryption at rest. Applications on several Linux instances use it all day. The company must encrypt the data, and it wants as little disruption as possible, with no data loss. What should a solutions architect do?

- A. Create a new encrypted EFS file system, copy the data with AWS DataSync, and switch clients over
- B. Enable default encryption for the account in the EFS console, which converts it
- C. Turn on encryption at rest in the file system's settings
- D. Mount the file system using TLS

> [!success]- Answer
> **A.** Encryption at rest is set when a file system is created, so a new one is needed, and DataSync copies the data. TLS protects data in transit only. Default settings affect only new file systems.
>
> *Task 1.3.* Review: [[08 Block and File Storage#Amazon EFS|Amazon EFS]]

**59.** A news site's web tier has a slow, predictable rise in traffic every morning. It also gets sudden, unplanned surges when stories spread on social media. New instances take four minutes to start serving. The team wants capacity in place for the morning rise, and a fast reaction to surprises, with nobody on call. Which combination should a solutions architect use? (Choose two.)

- A. Simple scaling with a one-hour cooldown
- B. Predictive scaling for the daily pattern
- C. A larger launch template version with no scaling policy
- D. Manual scaling by an on-call engineer
- E. Target tracking on requests per target for sudden surges

> [!success]- Answer
> **B and E.** Predictive scaling prepares for the pattern, and target tracking reacts to surprises. Manual scaling is slow. A long cooldown prevents quick reactions.
>
> *Task 3.2.* Review: [[05 Load Balancing and Auto Scaling#Scaling policies|Scaling policies]]

**60.** A gaming company stores player assets in S3, and its application reads about 30,000 objects per second from one bucket. All keys share a single prefix, `assets/`, and requests have started to be throttled at peak. The team wants to keep using S3 directly, and to spread reads evenly. What is the minimum number of prefixes needed?

- A. 2
- B. 4
- C. 12
- D. 6

> [!success]- Answer
> **D.** Each prefix supports at least 5,500 GET requests per second, and 30,000 divided by 5,500 is about 5.5, which rounds up to 6.
>
> *Task 3.1.* Review: [[06 Amazon S3#Performance|Performance]]

**61.** A company runs hundreds of Lambda functions written in pure Python, with no native libraries. Usage is steady all year, and it will continue for at least three years. Lambda has become the largest item on the bill, and the team has been asked to lower it without rewriting any code. Which two actions reduce cost with the least change? (Choose two.)

- A. Increase the memory of all functions
- B. Add provisioned concurrency to all functions
- C. Move all functions into a VPC
- D. Switch the functions to the arm64 architecture
- E. Buy a Compute Savings Plan

> [!success]- Answer
> **D and E.** Graviton gives better price-performance, and pure Python usually needs no change. Compute Savings Plans cover Lambda. More memory or provisioned concurrency adds cost, and a VPC adds no saving.
>
> *Task 4.2.* Review: [[16 Lambda and Serverless#Limits|Limits]]

**62.** An IoT platform must run a short validation workflow for each of about 100,000 events per second, with several steps and basic error handling. Each workflow finishes in under a minute, and the steps are idempotent, so duplicate runs are harmless. The team wants a managed orchestration service at the lowest possible cost. Which option fits?

- A. AWS Step Functions Standard workflows
- B. An EC2 cron job
- C. Amazon SWF
- D. AWS Step Functions Express workflows

> [!success]- Answer
> **D.** Express suits high-volume, short, idempotent work, at a low cost per run. Standard charges per state transition and is meant for long, durable workflows. SWF is an older service. A cron job does not suit event volumes.
>
> *Task 2.1.* Review: [[20 Messaging and Integration#AWS Step Functions|AWS Step Functions]]

**63.** A serverless API built on API Gateway, Lambda and a NoSQL database serves customers in Europe and North America. It must stay available if an entire Region fails. Customers should reach the nearest healthy Region, and writes must be accepted in both Regions at all times. Which two choices fit? (Choose two.)

- A. A single API Gateway in one Region, with CloudFront
- B. DynamoDB global tables
- C. DynamoDB with cross-Region backups only
- D. Aurora Global Database with writes in both Regions
- E. Route 53 latency routing with health checks to API Gateway in both Regions

> [!success]- Answer
> **B and E.** Global tables accept writes in each Region, and latency routing with health checks picks a healthy Region. Aurora Global has one writer Region. One API is still a single Region. Backups do not give an active second Region.
>
> *Task 2.2.* Review: [[14 DynamoDB#Global tables|Global tables]]

**64.** A company has 200 million objects of about 50 KB each, and they are rarely read. It plans a lifecycle rule to move them to Glacier Deep Archive to save money. What is the main concern, and what should it do?

- A. Lifecycle rules do not work on objects under 128 KB
- B. Deep Archive cannot store small objects, so use S3 Standard
- C. Small objects cannot be restored from Deep Archive
- D. Per-object transition charges and overhead are high for small objects, so combine them into larger archive files first

> [!success]- Answer
> **D.** Each object costs a transition request and adds 40 KB of overhead, so large numbers of small objects can cost more than they save. Lifecycle rules skip objects under 128 KB by default, so these 50 KB objects would not transition at all unless the rule is changed. Deep Archive can store them, but it is not cost-effective unless they are combined.
>
> *Task 4.1.* Review: [[06 Amazon S3#Storage classes|Storage classes]]

**65.** A company has 20 VPCs, each with NAT gateways in three AZs, all attached to a Transit Gateway. Internet traffic from each VPC is small. It wants to reduce the fixed hourly cost of NAT, and to inspect outbound traffic in one place. What should it consider?

- A. Send outbound traffic through a shared egress VPC with NAT gateways, using Transit Gateway routes
- B. Replace the Transit Gateway with VPC peering between all VPCs
- C. Add a NAT gateway to each subnet
- D. Attach an internet gateway to every private subnet

> [!success]- Answer
> **A.** A shared egress VPC reduces the number of NAT gateways. Transit Gateway data charges are added, so this suits low traffic. Peering has no edge-to-edge routing, so it cannot share NAT.
>
> *Task 4.4.* Review: [[29 Cost Optimisation#Network costs|Network costs]]

## Score your exam

Mark your answers with the key, then count your correct answers for each domain.

> [!example]- Answer key
> 1: C · 2: C · 3: C · 4: D · 5: C · 6: C · 7: A · 8: A · 9: D · 10: C  
> 11: B · 12: B · 13: C · 14: D · 15: C · 16: D · 17: A · 18: D · 19: A · 20: A  
> 21: B, E · 22: D · 23: B · 24: B · 25: D · 26: C · 27: A · 28: B · 29: A · 30: D  
> 31: A · 32: D · 33: B · 34: C · 35: A · 36: A, B · 37: D · 38: D · 39: B · 40: A  
> 41: B · 42: B · 43: A · 44: C · 45: A · 46: B · 47: D · 48: A · 49: B · 50: C, E  
> 51: A · 52: B · 53: B, E · 54: C · 55: D · 56: B · 57: D · 58: A · 59: B, E · 60: D  
> 61: D, E · 62: D · 63: B, E · 64: D · 65: A  

| Domain | Questions | Your score |
| --- | --- | --- |
| Domain 1: Secure | 4, 10, 13, 18, 21, 22, 23, 24, 27, 34, 35, 36, 37, 38, 41, 47, 48, 52, 54, 58 | ___ / 20 |
| Domain 2: Resilient | 1, 3, 5, 6, 11, 14, 29, 30, 32, 40, 49, 50, 53, 56, 57, 62, 63 | ___ / 17 |
| Domain 3: High-Performing | 7, 8, 9, 12, 16, 19, 20, 28, 31, 43, 44, 45, 55, 59, 60 | ___ / 15 |
| Domain 4: Cost-Optimized | 2, 15, 17, 25, 26, 33, 39, 42, 46, 51, 61, 64, 65 | ___ / 13 |
| **Total** | | **___ / 65** |

Add your result to the table in the [[Study Guide#Tracking your progress|Study Guide]], and every mistake to the [[Mistake Log]].

---
**Previous:** [[Practice Exam 4]] · **Plan:** [[Study Guide]]
