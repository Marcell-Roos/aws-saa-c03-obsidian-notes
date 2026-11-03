---
tags: [practice, scope/in]
---

# Practice Exam 1

> [!info] How to sit this exam
> - Set a timer for **130 minutes**, and sit it in one go, with no notes.
> - Write your answers on paper or in another note, and do not open the answers until you finish.
> - There are 65 questions. The real exam has 15 unscored questions, but all of these count here.
> - Score it with the table at the end, then review every question.
> - Aim for **80% or more** (52 of 65). See the [[Study Guide#Step 12 The readiness gate|readiness gate]].
>
> These are original practice questions written for this vault. They are not real exam questions, their difficulty has not been calibrated against the real exam, and real questions are often longer, so expect to do more reading on the day.

**1.** Instances in a VPC send 50 TB per month to S3 through a NAT gateway, in the same Region. What is the simplest way to reduce this cost?

- A. Create an interface endpoint for S3
- B. Order an AWS Direct Connect connection
- C. Create an S3 gateway endpoint, and update the route tables
- D. Replace the NAT gateway with a NAT instance

> [!success]- Answer
> **C.** Gateway endpoints are free. A NAT instance still costs money and adds management. An interface endpoint has hourly and per-GB charges. Direct Connect is for on-premises links.
>
> *Task 4.4.* Review: [[29 Cost Optimisation#Network costs|Network costs]]

**2.** A company must back up EC2, EFS, RDS and DynamoDB every day, and keep the backups for seven years. Backups must be protected from deletion, even if an administrator's credentials are stolen. Which solution meets these requirements?

- A. Use AWS Backup with Vault Lock in governance mode
- B. Write a Lambda function that creates snapshots, and restrict it with IAM
- C. Use AWS Backup with a backup plan, and apply Vault Lock in compliance mode
- D. Use Amazon Data Lifecycle Manager for all the resources

> [!success]- Answer
> **C.** AWS Backup covers all these services, and compliance mode cannot be removed by anyone after the grace period. Data Lifecycle Manager handles EBS snapshots and AMIs only. IAM restrictions can be changed by a compromised administrator, and governance mode can be removed with the right permissions.
>
> *Task 1.3.* Review: [[28 High Availability and Disaster Recovery#AWS Backup|AWS Backup]]

**3.** An application runs in two Regions. Traffic should go to the second Region only if the first is unhealthy. Which Route 53 configuration meets this requirement?

- A. Failover routing with a health check on the primary record
- B. Multivalue answer routing
- C. Latency routing with no health checks
- D. Weighted routing with equal weights

> [!success]- Answer
> **A.** Failover routing is active-passive by design. Equal weights split traffic. Latency routing sends users to both Regions all the time. Multivalue returns several records.
>
> *Task 2.2.* Review: [[11 Route 53#Failover|Failover]]

**4.** A payment service publishes events. Separate fraud, email and ledger systems must each process the events that matter to them, independently, and each must be able to retry failures. More consumers will be added later. Which design is best?

- A. Have the payment service call each system synchronously
- B. Send all events to one SQS queue that all three systems read from
- C. Publish to an SNS topic with a separate SQS queue for each consumer, using filter policies
- D. Have one Lambda function call each system in turn

> [!success]- Answer
> **C.** Fan-out gives each consumer its own durable queue, and filter policies send only relevant events. In a shared queue, each message goes to one consumer. Synchronous calls couple the services. A single function is a coupling point, and it is hard to extend.
>
> *Task 2.1.* Review: [[20 Messaging and Integration#Fan-out|Fan-out]]

**5.** Regulators require trade records in S3 to be impossible to change or delete for five years, even by the root user. Which solution meets this requirement?

- A. Enable S3 Object Lock in Governance mode, with a five-year retention period
- B. Add a bucket policy that denies `s3:DeleteObject` to all principals
- C. Enable versioning and MFA Delete on the bucket
- D. Enable S3 Object Lock in Compliance mode, with a five-year retention period

> [!success]- Answer
> **D.** In Compliance mode nobody can delete a locked version until the retention period ends. Governance mode can be bypassed with a permission. MFA Delete can be turned off by root. A bucket policy can be edited by an administrator.
>
> *Task 1.3.* Review: [[07 S3 Security and Data Protection#S3 Object Lock|S3 Object Lock]]

**6.** Private subnets in three AZs use one zonal NAT gateway in AZ-a. During an AZ-a outage, instances in the other two AZs lost internet access. What should a solutions architect do?

- A. Choose a larger NAT gateway size
- B. Move the instances into public subnets
- C. Deploy a NAT gateway in each AZ, and route each private subnet to the gateway in its own AZ
- D. Attach a second internet gateway to the VPC

> [!success]- Answer
> **C.** A zonal NAT gateway fails with its AZ, so each AZ needs its own. A VPC has one internet gateway. NAT gateways scale automatically and have no size. Public subnets expose the instances.
>
> *Task 2.2.* Review: [[09 VPC Fundamentals#NAT gateway|NAT gateway]]

**7.** An e-commerce company runs a relational database in us-east-1. It needs a disaster recovery site in eu-west-1 with an RPO of seconds and recovery in minutes, and it wants low-latency reads for European users. What should a solutions architect recommend?

- A. DynamoDB global tables
- B. Amazon Aurora Global Database
- C. RDS Multi-AZ
- D. RDS with snapshots copied to eu-west-1 every hour

> [!success]- Answer
> **B.** Aurora Global Database replicates across Regions at the storage layer and supports readers there. Multi-AZ stays in one Region. Hourly snapshots give an RPO of an hour. DynamoDB is not relational.
>
> *Task 2.2.* Review: [[13 RDS and Aurora#Aurora Global Database|Aurora Global Database]]

**8.** A legacy Linux application runs on one EC2 instance and writes uploaded files to a local directory. The code cannot be changed. The company wants it to survive an AZ failure, with several instances behind a load balancer sharing the same files. What should a solutions architect do?

- A. Attach one EBS volume to all the instances with Multi-Attach
- B. Sync the directory between instances with a nightly cron job
- C. Store the files on instance store volumes, and enable sticky sessions
- D. Mount an Amazon EFS file system at that directory on instances in an Auto Scaling group across AZs

> [!success]- Answer
> **D.** EFS is mounted like a normal directory, so no code changes are needed, and it works across AZs. Multi-Attach is limited to one AZ, and it needs a cluster-aware file system. A nightly sync loses recent files. Instance store data is lost with the instance.
>
> *Task 2.2.* Review: [[28 High Availability and Disaster Recovery#Making legacy applications more reliable|Making legacy applications more reliable]]

**9.** During database failovers, an application suffers long outages while thousands of connections are rebuilt. The application code cannot be changed, except for its connection string. What should a solutions architect do?

- A. Increase `max_connections` on the database
- B. Add read replicas
- C. Put Amazon RDS Proxy in front of the database
- D. Move the application to Lambda

> [!success]- Answer
> **C.** RDS Proxy keeps a pool of connections and reduces failover time, and it needs no code changes. Read replicas do not help writes reconnect. More connections do not shorten recovery. Moving to Lambda is a rewrite.
>
> *Task 2.2.* Review: [[13 RDS and Aurora#RDS Proxy|RDS Proxy]]

**10.** Logs are read often for 30 days, and rarely for the next 90 days, when they must still be available in milliseconds. After that they are kept for seven years for audit, and retrieval within 48 hours is acceptable. Which is the most cost-effective design?

- A. Store all the logs in S3 One Zone-IA for seven years
- B. Keep all the logs in S3 Standard for seven years
- C. Use S3 Standard, then Glacier Deep Archive at 30 days
- D. S3 Standard, then Standard-IA at 30 days, then Glacier Deep Archive at 120 days, and expire at seven years

> [!success]- Answer
> **D.** The pattern is known, so lifecycle rules fit, and each period uses the cheapest suitable class. Staying in Standard costs more. One Zone-IA risks audit data. Deep Archive at 30 days breaks the millisecond requirement.
>
> *Task 4.1.* Review: [[06 Amazon S3#Lifecycle rules|Lifecycle rules]]

**11.** A DynamoDB table serves a read-heavy application with some very popular items. Reads must take microseconds, and code changes must be minimal. What should a solutions architect recommend?

- A. Increasing the table's provisioned read capacity
- B. DynamoDB Accelerator (DAX)
- C. Amazon ElastiCache with a lazy loading strategy
- D. DynamoDB read replicas

> [!success]- Answer
> **B.** DAX is a DynamoDB-compatible cache with microsecond reads. ElastiCache needs more code changes. DynamoDB has no read replicas. More capacity does not reach microseconds.
>
> *Task 3.3.* Review: [[14 DynamoDB#DynamoDB Accelerator|DynamoDB Accelerator]]

**12.** An order website receives ten times its normal traffic during promotions. The web tier scales well, but the order-processing tier falls behind and orders time out. Orders must not be lost. What should a solutions architect do?

- A. Put an SQS queue between the tiers, and scale an Auto Scaling group of workers on the backlog per instance
- B. Add an SNS topic with an email subscription for each order
- C. Move the order-processing tier to larger EC2 instances
- D. Increase the idle timeout on the Application Load Balancer

> [!success]- Answer
> **A.** The queue buffers the spike and holds orders until workers catch up, and the workers scale with the backlog. Larger instances still have a limit. Emails do not process orders. A longer timeout does not add capacity.
>
> *Task 2.1.* Review: [[20 Messaging and Integration#Scaling workers on queue depth|Scaling workers on queue depth]]

**13.** Each file uploaded to S3 must be processed by a containerised job that takes up to 40 minutes. The company prefers not to manage servers. What should a solutions architect recommend?

- A. Use an Amazon EventBridge rule to run an ECS task on AWS Fargate when a file arrives
- B. Run the job on Reserved Instances that poll the bucket
- C. Trigger an AWS Lambda function from the S3 event
- D. Use API Gateway to call the container when files arrive

> [!success]- Answer
> **A.** Fargate tasks have no 15-minute limit, and EventBridge can start them on S3 events. Lambda stops at 15 minutes. Polling Reserved Instances means servers to manage and idle capacity. API Gateway is not an event source for S3.
>
> *Task 2.1.* Review: [[18 Containers#Event-driven patterns|Event-driven patterns]]

**14.** Account A has an EBS snapshot encrypted with a customer managed KMS key. Account B must create volumes from that snapshot. What should a solutions architect do? (Choose two.)

- A. Update the KMS key policy to allow Account B to use the key
- B. Share the snapshot with Account B
- C. Copy the AWS managed key into Account B
- D. Make the snapshot public
- E. Disable encryption on the snapshot

> [!success]- Answer
> **A and B.** Account B needs access to the snapshot and to the key that protects it. Public snapshots cannot be encrypted. AWS managed keys cannot be shared or copied. Encryption cannot be removed from a snapshot in place.
>
> *Task 1.3.* Review: [[23 Encryption and Secrets#Key policies|Key policies]]

**15.** A company hires an external security vendor that uses one AWS account to assess many customers. The vendor needs read-only access to the company's AWS account. The company must not share long-term credentials, and it must make sure that the vendor's other customers cannot trick the vendor into reaching the company's account. What should a solutions architect do?

- A. Invite the vendor's account into the company's organisation, and attach a read-only SCP
- B. Export the configuration of all resources to an S3 bucket, and add a bucket policy for the vendor's account
- C. Create an IAM user with a read-only policy, and give the vendor its access keys
- D. Create an IAM role with a read-only policy, and a trust policy for the vendor's account that requires an ExternalId

> [!success]- Answer
> **D.** A cross-account role gives temporary credentials, and the ExternalId prevents the confused deputy problem. An IAM user's keys are long-term credentials. Joining the organisation gives far more access than needed, and an SCP does not grant anything. Exporting data is not read-only account access and is hard to keep current.
>
> *Task 1.1.* Review: [[02 IAM and Federation#Cross-account access|Cross-account access]]

**16.** A trading platform uses a custom TCP protocol. It needs to handle millions of requests per second at very low latency, and clients must connect to fixed IP addresses in each AZ. Which load balancer fits?

- A. Classic Load Balancer
- B. Gateway Load Balancer
- C. Network Load Balancer
- D. Application Load Balancer

> [!success]- Answer
> **C.** An NLB handles TCP at layer 4 with very low latency and one static IP per AZ. An ALB is for HTTP and has no static IPs. A GWLB is for appliances. The Classic Load Balancer is a previous-generation product.
>
> *Task 3.4.* Review: [[05 Load Balancing and Auto Scaling#Network Load Balancer|Network Load Balancer]]

**17.** A DynamoDB table in provisioned mode must support 100 strongly consistent reads per second of items that are 6 KB in size. How many read capacity units are needed?

- A. 200
- B. 100
- C. 400
- D. 150

> [!success]- Answer
> **A.** 6 KB rounds up to 8 KB, which is 2 RCU per strongly consistent read, so 100 reads need 200 RCU. Eventually consistent reads would need half of that, which is 100.
>
> *Task 3.3.* Review: [[14 DynamoDB#Calculating capacity|Calculating capacity]]

**18.** An application on EC2 reads a database password at start-up. A security audit requires that the password is not stored on the instance, and that it rotates automatically every 30 days with no custom scheduling work. What should a solutions architect recommend?

- A. Store the password in a Parameter Store String parameter, and change it manually each month
- B. Store the password in an encrypted S3 object, and put an access key on the instance to read it
- C. Pass the password in EC2 user data, and replace the instances every 30 days
- D. Store the password in AWS Secrets Manager with rotation enabled, and allow the instance role to read the secret

> [!success]- Answer
> **D.** Secrets Manager has built-in rotation, and the instance role avoids stored credentials. Parameter Store has no native rotation. An access key on the instance is what the audit is trying to remove. User data is readable from the instance and is not a secret store.
>
> *Task 1.2.* Review: [[23 Encryption and Secrets#AWS Secrets Manager|AWS Secrets Manager]]

**19.** A global voice application uses UDP, and it runs in two Regions. It needs low latency, and traffic must move quickly away from an unhealthy Region. What should a solutions architect recommend?

- A. Amazon CloudFront in front of both Regions
- B. Route 53 latency routing to an ALB in each Region
- C. S3 Transfer Acceleration
- D. AWS Global Accelerator with endpoint groups in both Regions

> [!success]- Answer
> **D.** Global Accelerator supports UDP, uses the AWS backbone and shifts traffic with no DNS change. CloudFront handles HTTP. An ALB does not support UDP. Transfer Acceleration is for S3.
>
> *Task 3.4.* Review: [[12 CloudFront and Global Accelerator#AWS Global Accelerator|AWS Global Accelerator]]

**20.** A company runs EC2 in several Regions, plus Fargate and Lambda, and it expects to change instance families. It wants to commit for three years to lower its compute bill. Which option fits?

- A. Standard Reserved Instances
- B. EC2 Instance Savings Plan
- C. Spot Instances
- D. Compute Savings Plan

> [!success]- Answer
> **D.** Compute Savings Plans apply across Regions, families, Fargate and Lambda. An EC2 Instance Savings Plan is tied to a family and Region. Standard RIs are not flexible. Spot is not a commitment and can be interrupted.
>
> *Task 4.2.* Review: [[04 Amazon EC2#Savings Plans|Savings Plans]]

**21.** A company wants to stop paying for Oracle licences by moving to an open-source engine on AWS, with minimal downtime. What should a solutions architect recommend?

- A. Move to RDS for Oracle with bring your own licence
- B. Convert the schema with AWS SCT or DMS Schema Conversion, and migrate to Aurora PostgreSQL with AWS DMS using ongoing replication
- C. Move Oracle to EC2 and use Spot Instances
- D. Migrate the data to Amazon DynamoDB using S3

> [!success]- Answer
> **B.** This removes the licence, and ongoing replication keeps downtime low. RDS for Oracle and Oracle on EC2 keep the licence. Spot is unsuitable for a database. DynamoDB would need a rewrite.
>
> *Task 4.3.* Review: [[27 Migration and Data Transfer#AWS DMS|AWS DMS]]

**22.** A company connects its data centre to a VPC with AWS Direct Connect. A new compliance rule says that all traffic between them must be encrypted with IPsec. What should a solutions architect do?

- A. Use a private virtual interface, because Direct Connect traffic is private
- B. Enable default encryption for all S3 buckets and EBS volumes
- C. Establish an AWS Site-to-Site VPN over the Direct Connect connection
- D. Enable VPC Flow Logs on all subnets

> [!success]- Answer
> **C.** A VPN over Direct Connect adds IPsec. Private is not the same as encrypted. Encrypting storage protects data at rest and does nothing for traffic. Flow logs are a monitoring tool.
>
> *Task 1.2.* Review: [[10 VPC Connectivity and Hybrid Networking#Encryption|Encryption]]

**23.** Windows application servers need a shared file system with Active Directory permissions, which must remain available if an AZ fails. What should a solutions architect recommend?

- A. Amazon EFS with a Regional file system
- B. Amazon FSx for Windows File Server with a Multi-AZ deployment
- C. Amazon FSx for Lustre with Scratch storage
- D. S3 File Gateway on an EC2 instance

> [!success]- Answer
> **B.** FSx for Windows provides SMB, Active Directory integration and Multi-AZ failover. EFS does not support Windows. A gateway is for on-premises access. Lustre is for HPC on Linux.
>
> *Task 3.1.* Review: [[08 Block and File Storage#FSx for Windows File Server|FSx for Windows File Server]]

**24.** A company runs RDS for MySQL in a single AZ. It needs automatic failover if the AZ fails, with no change to the database endpoint used by the application. What should a solutions architect do?

- A. Copy manual snapshots to another AZ every hour
- B. Create a cross-Region read replica
- C. Create a read replica in another AZ
- D. Convert the database to a Multi-AZ deployment

> [!success]- Answer
> **D.** Multi-AZ gives a synchronous standby and flips the DNS name automatically. Read replicas need manual promotion and have their own endpoint. Restoring from snapshots takes time, and it creates a new endpoint.
>
> *Task 2.2.* Review: [[13 RDS and Aurora#Multi-AZ|Multi-AZ]]

**25.** A Lambda function that resizes images is CPU-bound and takes too long. What is the simplest way to speed it up?

- A. Set reserved concurrency
- B. Increase the function's timeout
- C. Increase the function's memory setting
- D. Add a Lambda layer

> [!success]- Answer
> **C.** Lambda allocates CPU in proportion to memory. A layer adds code. Reserved concurrency controls parallel copies, not speed. A longer timeout only allows the function to run longer.
>
> *Task 3.2.* Review: [[16 Lambda and Serverless#Limits|Limits]]

**26.** IoT sensors send records that must be processed in real time by two separate applications. Records must be replayable for up to seven days. What should a solutions architect recommend?

- A. An Amazon SNS topic
- B. An Amazon SQS standard queue
- C. Amazon Kinesis Data Streams with retention set to seven days
- D. Amazon Data Firehose delivering to S3

> [!success]- Answer
> **C.** Kinesis Data Streams allows several independent consumers and replay. Firehose buffers and delivers, and offers no replay. An SQS message goes to one consumer and is deleted. A standard SNS topic delivers messages to subscribers and does not hold them for replay.
>
> *Task 3.5.* Review: [[21 Streaming and Data Ingestion#Kinesis Data Streams|Kinesis Data Streams]]

**27.** A team keeps a `t3.small` instance running all day only to run a five-minute report script at 01:00. What should a solutions architect recommend to reduce cost and operational work?

- A. Use an Amazon EventBridge schedule to invoke an AWS Lambda function
- B. Run the script from an Elastic Beanstalk worker environment
- C. Move the script to a Spot Instance with a crontab entry
- D. Buy a Reserved Instance for the `t3.small`

> [!success]- Answer
> **A.** A scheduled Lambda function removes the idle server. Spot still needs an instance waiting for the time to arrive. A Reserved Instance pays for idle time. Beanstalk adds more infrastructure than a five-minute job needs.
>
> *Task 2.1.* Review: [[16 Lambda and Serverless#Scheduled jobs|Scheduled jobs]]

**28.** A company needs HTTPS on a public Application Load Balancer. The certificate must renew automatically, with no manual steps. Which solution meets this requirement?

- A. Buy a certificate from a third party, and import it into ACM
- B. Request a public certificate from ACM with DNS validation, and attach it to an HTTPS listener
- C. Request a public certificate from ACM with email validation
- D. Generate a self-signed certificate on each instance

> [!success]- Answer
> **B.** DNS-validated ACM certificates renew automatically while in use. Imported certificates are not renewed by ACM. Email validation needs someone to respond. Self-signed certificates are not trusted by browsers.
>
> *Task 1.3.* Review: [[23 Encryption and Secrets#AWS Certificate Manager|AWS Certificate Manager]]

**29.** Team leads must be able to create IAM roles for their Lambda functions without waiting for the security team. Security requires that no role created this way can ever have more than S3 and DynamoDB access. What should a solutions architect do?

- A. Attach an SCP that allows only S3 and DynamoDB to the account
- B. Give the team leads `AdministratorAccess`, and review role permissions every week with Access Advisor
- C. Allow `iam:CreateRole` only when a defined permission boundary is attached to the new role
- D. Require the team leads to submit each role to the security team for creation

> [!success]- Answer
> **C.** A condition on `iam:PermissionsBoundary` lets the leads create roles, while the boundary caps what those roles can do. A weekly review only finds problems later. The SCP would restrict everyone in the account, not just the new roles. Central creation brings back the wait that the company wants to remove.
>
> *Task 1.1.* Review: [[02 IAM and Federation#Permission boundaries|Permission boundaries]]

**30.** A company has 300 S3 buckets and must find which ones contain credit card numbers, and alert the security team. Which solution requires the least effort?

- A. Use Amazon Macie, and send findings through Amazon EventBridge to an SNS topic
- B. Write AWS Glue jobs to scan each bucket for patterns
- C. Use Amazon GuardDuty S3 Protection, and review the console daily
- D. Use Amazon Inspector to scan each bucket

> [!success]- Answer
> **A.** Macie is built to find sensitive data in S3, and its findings can drive alerts. GuardDuty detects threats and not data types. Inspector scans workloads for vulnerabilities. Custom Glue jobs are much more work.
>
> *Task 1.3.* Review: [[24 Threat Protection and Security Services#Amazon Macie|Amazon Macie]]

**31.** A healthcare company stores records in Amazon S3. Requirements are encryption at rest, separate permission to use the key, an audit trail of each use of the key, and annual rotation. Which option requires the least effort and meets these requirements?

- A. Use SSE-C with keys held by the application
- B. Use SSE-S3
- C. Use client-side encryption with a key stored in the application's code
- D. Use SSE-KMS with a customer managed key that has automatic rotation enabled

> [!success]- Answer
> **D.** SSE-KMS gives key-level permissions, CloudTrail logging and rotation. SSE-S3 does not provide a separate key permission or key use audit. SSE-C leaves key management to you. A key in code is insecure and adds work.
>
> *Task 1.3.* Review: [[07 S3 Security and Data Protection#Encryption at rest|Encryption at rest]]

**32.** An audit finds that a production RDS for PostgreSQL database is not encrypted. The company must encrypt it with as little downtime as is practical. What should a solutions architect do?

- A. Take a snapshot, copy it with encryption enabled, restore it to a new database, and move the application to it
- B. Create an encrypted read replica, then promote it
- C. Turn on the `rds.force_ssl` parameter
- D. Modify the database to enable encryption, and reboot

> [!success]- Answer
> **A.** Encryption is chosen at creation, so a new encrypted database is needed. There is no in-place option. You cannot create an encrypted replica of an unencrypted database. Forcing SSL protects data in transit, not at rest.
>
> *Task 1.3.* Review: [[13 RDS and Aurora#Security|Security]]

**33.** Development teams use relational databases for a few hours a day, at unpredictable times, and pay for them around the clock. Which option reduces cost with the least administration?

- A. RDS with Reserved Instances
- B. Amazon DynamoDB
- C. Amazon Aurora Serverless v2
- D. Provisioned RDS Multi-AZ

> [!success]- Answer
> **C.** Aurora Serverless v2 scales with demand and can scale to zero. Multi-AZ doubles the cost and adds nothing here. RIs commit you to always-on capacity. DynamoDB would mean rewriting the application.
>
> *Task 4.3.* Review: [[13 RDS and Aurora#Aurora Serverless v2|Aurora Serverless v2]]

**34.** Logs show that one external IP range is attacking a public ALB. The security team must block that range at the subnet level straight away, while allowing all other traffic. What should a solutions architect do?

- A. Add a deny rule for the range to the network ACL, with a higher rule number than the rule that allows traffic
- B. Add a deny rule for the range to the network ACL of the ALB's subnets, with a lower rule number than the rule that allows traffic
- C. Add a deny rule for the range to the ALB's security group
- D. Add a route to the range with a blackhole target in the VPC route table

> [!success]- Answer
> **B.** NACL rules are evaluated from the lowest number, and the first match wins, so the deny must come before the allow. Security groups cannot deny. A higher number would never be reached. A route table affects where outbound traffic goes, so it does not stop inbound requests.
>
> *Task 1.2.* Review: [[09 VPC Fundamentals#Network ACLs|Network ACLs]]

**35.** A company must copy 8 TB to S3 once. It has a mostly idle 1 Gbps internet connection, and five days to finish. What is the most cost-effective method?

- A. Set up a second internet link just for this transfer
- B. Order an AWS Snowball Edge device
- C. Upload over the existing internet connection, using multipart uploads or AWS DataSync
- D. Order a new AWS Direct Connect connection

> [!success]- Answer
> **C.** 8 TB at 1 Gbps takes under a day, so the existing link is enough. Direct Connect takes weeks to set up. A device costs more and takes longer. A new link is not needed.
>
> *Task 4.1.* Review: [[27 Migration and Data Transfer#Choosing a transfer method|Choosing a transfer method]]

**36.** A company has created a new AWS account. Which two actions should it take first to secure the root user? (Choose two.)

- A. Share the root password with two administrators, in case of an emergency
- B. Store root access keys in AWS Secrets Manager for applications to use
- C. Make sure that the root user has no access keys
- D. Enable MFA on the root user
- E. Use the root user for daily administration, with a strong password

> [!success]- Answer
> **C and D.** MFA and having no root access keys are the first steps. Daily work should use a federated or least-privilege identity. Sharing the password removes accountability. Applications should use roles, never root keys.
>
> *Task 1.1.* Review: [[02 IAM and Federation#The root user|The root user]]

**37.** Users in Asia see slow reads from an RDS for MySQL database in Ireland. Writes can stay in Ireland, and most traffic is reads. What should a solutions architect recommend?

- A. Scale the database to a larger instance
- B. Enable Multi-AZ on the database
- C. Replicate the database with S3 Cross-Region Replication
- D. Create a cross-Region read replica in Asia, and send local reads to it

> [!success]- Answer
> **D.** A local replica gives Asian users lower read latency. Multi-AZ stays in the Region. A bigger instance does not remove network distance. S3 replication does not apply to databases.
>
> *Task 3.3.* Review: [[13 RDS and Aurora#Read replicas|Read replicas]]

**38.** A public website behind Amazon CloudFront is receiving SQL injection attempts, and scrapers are sending thousands of requests per minute from single IP addresses. What should a solutions architect do?

- A. Attach an AWS WAF web ACL to the distribution, with a managed rule group for SQL injection and a rate-based rule
- B. Rely on AWS Shield Standard, which filters these requests automatically
- C. Enable Amazon GuardDuty, and use EventBridge to send an email alert
- D. Add network ACL rules to the origin's subnets to block the IP addresses

> [!success]- Answer
> **A.** WAF inspects HTTP requests at layer 7, and rate-based rules limit requests per IP. Shield Standard covers network-layer DDoS. The origin sees CloudFront's addresses, so a NACL there cannot filter clients. GuardDuty detects threats, and it does not block web requests.
>
> *Task 1.2.* Review: [[24 Threat Protection and Security Services#AWS WAF|AWS WAF]]

**39.** Which two actions make a web tier resilient to the loss of an AZ? (Choose two.)

- A. Enable the Application Load Balancer in at least two AZs
- B. Replace the instances with one larger instance in a single AZ
- C. Assign an Elastic IP address to each instance
- D. Run an Auto Scaling group across at least two AZs
- E. Launch all instances in a cluster placement group

> [!success]- Answer
> **A and D.** Spreading instances and the load balancer across AZs removes the AZ as a single point of failure. A cluster placement group is in one AZ. One large instance is a single point of failure. Elastic IPs do not add availability.
>
> *Task 2.2.* Review: [[05 Load Balancing and Auto Scaling#Amazon EC2 Auto Scaling|Amazon EC2 Auto Scaling]]

**40.** A fleet uses 1 TiB gp2 volumes, and performance is fine. The company wants to reduce EBS cost without downtime. What should a solutions architect do?

- A. Change the volumes to gp3 using Elastic Volumes
- B. Change the volumes to io2
- C. Move the data to instance store
- D. Change the root volumes to sc1

> [!success]- Answer
> **A.** gp3 costs less per GiB, and Elastic Volumes change the type while the volume is in use. io2 costs more. sc1 cannot be a boot volume. Instance store loses data when an instance stops.
>
> *Task 4.1.* Review: [[08 Block and File Storage#Volume types|Volume types]]

**41.** A weather simulation runs on tightly coupled nodes, and it needs the lowest possible latency between them. Which two choices should a solutions architect make? (Choose two.)

- A. Launch the instances in a spread placement group
- B. Launch the instances in a cluster placement group
- C. Put a Network Load Balancer between the nodes
- D. Place the instances in several Regions
- E. Use instance types with an Elastic Fabric Adapter

> [!success]- Answer
> **B and E.** A cluster placement group keeps nodes close together, and EFA gives OS-bypass networking. A spread group separates instances. Multiple Regions add latency. A load balancer adds a hop.
>
> *Task 3.2.* Review: [[04 Amazon EC2#Fast networking|Fast networking]]

**42.** A stateless web tier needs 10 instances at all times, and up to 40 during unpredictable peaks. It can tolerate losing some of the extra instances. What is the most cost-effective approach?

- A. Run everything on Spot Instances
- B. Use Dedicated Hosts for all the instances
- C. Use Savings Plans or RIs for the base of 10, and Spot in a mixed instances Auto Scaling group for the rest
- D. Run everything on On-Demand Instances

> [!success]- Answer
> **C.** Commit to the steady base, and use Spot for the interruptible surge. On-Demand costs more. All Spot risks losing the base. Dedicated Hosts are for licensing and compliance.
>
> *Task 4.2.* Review: [[05 Load Balancing and Auto Scaling#Mixed instances|Mixed instances]]

**43.** A workload needs an RPO of one minute and an RTO of 15 minutes. The company wants to pay less than a full second production environment, and it is happy to run a small working copy of the application at all times. Which DR strategy fits?

- A. Warm standby
- B. Multi-site active-active
- C. Backup and restore
- D. Cold restore from AMIs when needed

> [!success]- Answer
> **A.** Warm standby runs a smaller functional copy that scales up on failover. Backup and restore cannot meet a 15-minute RTO. Active-active costs as much as full production. Building from AMIs when needed cannot meet the RPO without live data replication.
>
> *Task 2.2.* Review: [[28 High Availability and Disaster Recovery#Disaster recovery strategies|Disaster recovery strategies]]

**44.** A company uses AWS Organizations. It must make sure that nobody in its member accounts, including account administrators, can create resources outside eu-west-1. Global services such as IAM must continue to work. Which solution meets these requirements with the least ongoing effort?

- A. Attach an IAM policy to each user and role in each account that denies other Regions
- B. Attach a permission boundary to every user and role in each account
- C. Create an AWS Config rule that finds resources in other Regions, and delete them with a Lambda function
- D. Attach an SCP to the organisation's root or OU that denies actions outside eu-west-1 using `aws:RequestedRegion`, with global services excluded by `NotAction`

> [!success]- Answer
> **D.** An SCP applies to every principal in the affected accounts, including administrators, and it is inherited automatically. Per-identity policies and boundaries need constant maintenance and can be missed. A Config rule reacts after the event and does not prevent anything.
>
> *Task 1.1.* Review: [[03 Multi-Account Governance#Service control policies|Service control policies]]

**45.** A company has an on-premises Microsoft Active Directory. Employees must use their existing corporate credentials to sign in to 30 AWS accounts. The company wants permissions managed centrally and does not want to store user identities in AWS. Which solution meets these requirements?

- A. Create a Cognito user pool with SAML federation, and share it with all the accounts
- B. Create matching IAM users in each account, and enforce the same password policy
- C. Use IAM Identity Center connected to the on-premises directory through AD Connector, and assign permission sets to groups
- D. Deploy Simple AD, and create a trust with the on-premises directory

> [!success]- Answer
> **C.** Identity Center is built for workforce access to many accounts, and AD Connector forwards authentication without storing identities in AWS. IAM users duplicate identities. Cognito is for customers of applications. Simple AD does not support trusts and is closed to new customers.
>
> *Task 1.1.* Review: [[02 IAM and Federation#AWS IAM Identity Center|AWS IAM Identity Center]]

**46.** A transactional database on EC2 needs a sustained 150,000 IOPS, with sub-millisecond latency and high durability. The data must persist if the instance stops. Which storage should be used?

- A. EBS io2 Block Express volumes on a Nitro-based instance
- B. EBS st1 volumes
- C. Instance store volumes
- D. EBS gp3 volumes

> [!success]- Answer
> **A.** io2 Block Express reaches 256,000 IOPS with 99.999% durability. gp3 tops out at 80,000 IOPS. st1 is HDD. Instance store loses data when the instance stops.
>
> *Task 3.1.* Review: [[08 Block and File Storage#Volume types|Volume types]]

**47.** Administrators connect to private EC2 instances through a bastion host in a public subnet. The security team wants to close port 22, remove the bastion, and record all sessions. What should a solutions architect recommend?

- A. Use EC2 Instance Connect from the internet on public IP addresses
- B. Place a Network Load Balancer in front of the bastion host
- C. Connect through a VPN, and keep SSH open from the VPC
- D. Use AWS Systems Manager Session Manager, with instance roles and session logging to S3 or CloudWatch Logs

> [!success]- Answer
> **D.** Session Manager needs no inbound ports, no bastion and no SSH keys, and it can log sessions. Instance Connect still needs port 22. A VPN keeps SSH open. An NLB keeps the bastion.
>
> *Task 1.2.* Review: [[26 Infrastructure as Code and Operations#Session Manager|Session Manager]]

**48.** A data lake holds millions of objects, all over 1 MB, with unpredictable access patterns. Some objects are read daily, and others not for months. The company wants to lower cost with no retrieval charges and no performance impact. What should it use?

- A. S3 Intelligent-Tiering
- B. S3 Standard-IA
- C. S3 One Zone-IA
- D. S3 Glacier Instant Retrieval

> [!success]- Answer
> **A.** Intelligent-Tiering moves objects automatically and has no retrieval fees. The IA and Glacier classes charge for retrieval, which is risky when access is unknown, and One Zone-IA also loses resilience.
>
> *Task 4.1.* Review: [[06 Amazon S3#S3 Intelligent-Tiering|S3 Intelligent-Tiering]]

**49.** Two VPCs in the same Region exchange data. No other networks are involved. Which option has the lowest cost?

- A. AWS Site-to-Site VPN
- B. AWS Transit Gateway
- C. AWS PrivateLink
- D. VPC peering

> [!success]- Answer
> **D.** Peering has no hourly charge, and it suits a small number of VPCs. Transit Gateway charges per attachment and per GB. A VPN is for on-premises links, and PrivateLink is for exposing single services and is charged by the hour.
>
> *Task 4.4.* Review: [[29 Cost Optimisation#Connection choices|Connection choices]]

**50.** Analysts run Athena queries over JSON logs in S3, and each query scans all the data. Which two actions reduce cost and improve speed? (Choose two.)

- A. Partition the data by date in S3
- B. Move the data to S3 Glacier Deep Archive
- C. Enable S3 versioning
- D. Move the data to S3 Standard-IA
- E. Convert the data to Parquet using AWS Glue

> [!success]- Answer
> **A and E.** Columnar files and partitions reduce the data scanned, which is what Athena charges for. Deep Archive data cannot be queried directly. Standard-IA changes storage cost, and it adds retrieval charges. Versioning adds no benefit here.
>
> *Task 3.5.* Review: [[22 Data Lakes and Analytics#Amazon Athena|Amazon Athena]]

**51.** An Auto Scaling group sits behind an ALB. Response times rise as requests build up, yet average CPU stays low because the work is I/O-bound. Which scaling policy should be used?

- A. A step policy based on free disk space
- B. Target tracking on CPU at 90%
- C. Scheduled scaling at fixed times
- D. Target tracking on the `ALBRequestCountPerTarget` metric

> [!success]- Answer
> **D.** Requests per target reflect the actual load. A higher CPU target would scale even later. Disk space is unrelated. A fixed schedule does not follow unpredictable traffic.
>
> *Task 3.2.* Review: [[05 Load Balancing and Auto Scaling#Scaling policies|Scaling policies]]

**52.** A machine learning team keeps petabytes of training data in S3. Training runs on GPU instances for a few days at a time, and needs very high throughput to the data through a POSIX file system. What should a solutions architect recommend?

- A. Amazon EFS with lifecycle management
- B. EBS io2 with Multi-Attach
- C. S3 Glacier Flexible Retrieval
- D. Amazon FSx for Lustre linked to the S3 bucket

> [!success]- Answer
> **D.** Lustre presents S3 data as a high-speed parallel file system. EFS does not match this throughput for HPC. Glacier is for archives. Multi-Attach is limited to 16 instances in one AZ, and it is not a shared file system.
>
> *Task 3.1.* Review: [[08 Block and File Storage#FSx for Lustre|FSx for Lustre]]

**53.** Customers of a shopping site behind an ALB lose their carts when the Auto Scaling group scales in. The company wants the web tier to scale freely. What should a solutions architect do?

- A. Enable sticky sessions on the target group
- B. Disable scale-in on the Auto Scaling group
- C. Store session data in Amazon ElastiCache or DynamoDB
- D. Store session data on instance store volumes

> [!success]- Answer
> **C.** Keeping sessions outside the instances makes the tier stateless. Sticky sessions still lose data when an instance goes. Instance store disappears with the instance. Disabling scale-in wastes money and does not handle failures.
>
> *Task 2.1.* Review: [[31 Architecture Patterns#Stateless and stateful workloads|Stateless and stateful workloads]]

**54.** A company has 40 VPCs across three accounts, and two data centres. All must connect through a central point, with production and development kept apart. What should a solutions architect recommend?

- A. A full mesh of VPC peering connections
- B. AWS Transit Gateway shared through AWS RAM, with separate route tables for production and development
- C. Public IP addresses on all resources, with security groups
- D. AWS PrivateLink between each pair of VPCs

> [!success]- Answer
> **B.** Transit Gateway gives transitive routing, and its route tables provide segmentation. A full mesh of 40 VPCs needs 780 peerings. PrivateLink exposes single services. Public addresses are not a private network.
>
> *Task 3.4.* Review: [[10 VPC Connectivity and Hybrid Networking#AWS Transit Gateway|AWS Transit Gateway]]

**55.** A company is splitting a monolith into containerised microservices. All must be served under one domain, with `/users` and `/orders` going to different services. Each service must scale independently, and the company does not want to manage hosts. What should a solutions architect recommend?

- A. Run the services on EC2 behind a Network Load Balancer, with a listener for each service
- B. Use CloudFront signed URLs to direct traffic to each service
- C. Run all containers on one large EC2 instance using Docker Compose
- D. Run the services on Amazon ECS with AWS Fargate behind an Application Load Balancer, with a target group for each service and path-based rules

> [!success]- Answer
> **D.** ALB path routing plus ECS services on Fargate gives independent scaling with no hosts. An NLB cannot route on paths, and EC2 means hosts. One instance is a single point of failure. Signed URLs control access and do not route traffic.
>
> *Task 2.1.* Review: [[18 Containers#Networking and load balancing|Networking and load balancing]]

**56.** Instances in private subnets must call AWS Secrets Manager and AWS KMS. Security policy forbids any route to the internet, including through NAT. What should a solutions architect do?

- A. Deploy a NAT instance in a public subnet with a restrictive security group
- B. Peer the VPC with another VPC that has an internet gateway
- C. Create interface VPC endpoints for Secrets Manager and KMS
- D. Create gateway VPC endpoints for Secrets Manager and KMS

> [!success]- Answer
> **C.** Interface endpoints give private access to most AWS services. Gateway endpoints exist only for S3 and DynamoDB. A NAT instance is still a route to the internet. Peering has no edge-to-edge routing, so it would not work either.
>
> *Task 1.2.* Review: [[10 VPC Connectivity and Hybrid Networking#VPC endpoints|VPC endpoints]]

**57.** A company must move 60 TB from an on-premises NFS server to Amazon EFS over Direct Connect. It must keep file metadata, and run nightly incremental copies until the final cutover. Which service fits?

- A. AWS Transfer Family
- B. AWS Snowball Edge
- C. AWS DataSync
- D. S3 File Gateway

> [!success]- Answer
> **C.** DataSync handles scheduled incremental transfers to EFS and preserves metadata. A Snow device does not suit nightly updates. A gateway provides ongoing access, not migration to EFS. Transfer Family is for SFTP-style file exchange.
>
> *Task 3.5.* Review: [[27 Migration and Data Transfer#AWS DataSync|AWS DataSync]]

**58.** Month-end reports slow down a production RDS for PostgreSQL database that already has Multi-AZ enabled. The application must not be affected by the reports. What should a solutions architect do?

- A. Point the reporting tool at the Multi-AZ standby
- B. Create a read replica, and point the reporting tool at it
- C. Add RDS Proxy in front of the database
- D. Increase the allocated storage

> [!success]- Answer
> **B.** A read replica takes the reporting load away from the primary. The standby of a Multi-AZ instance deployment cannot be read. More storage does not reduce load from queries. RDS Proxy manages connections and does not add read capacity.
>
> *Task 2.1.* Review: [[13 RDS and Aurora#Read replicas|Read replicas]]

**59.** An internal API receives about 2,000 requests a day, each taking under 200 ms, and it is idle overnight. It runs on two `m5.large` instances all the time. What should a solutions architect recommend to lower cost?

- A. Move the API to AWS Lambda with Amazon API Gateway
- B. Buy Reserved Instances for the two instances
- C. Move to Spot Instances
- D. Move to larger instances

> [!success]- Answer
> **A.** With such low traffic, paying per request is far cheaper than always-on servers. RIs still pay for idle time. Spot can interrupt an API. Larger instances cost more.
>
> *Task 4.2.* Review: [[16 Lambda and Serverless#When to use serverless|When to use serverless]]

**60.** Users report intermittent slowness in an API built from API Gateway, several Lambda functions and DynamoDB. The team needs to see which component is adding latency for each request. What should it use?

- A. AWS X-Ray
- B. AWS Config
- C. AWS CloudTrail
- D. VPC Flow Logs

> [!success]- Answer
> **A.** X-Ray traces requests across services. CloudTrail records API calls for audit. Config records resource configuration. Flow logs show network metadata.
>
> *Task 2.2.* Review: [[25 Monitoring and Auditing#AWS X-Ray|AWS X-Ray]]

**61.** A finance team stores reports in an S3 bucket. All accounts in the company's AWS organisation must be able to read them. The organisation has 200 accounts and adds new ones each month. What is the most operationally efficient way to grant access?

- A. Make the bucket public, and share the URL only with staff
- B. Add a bucket policy that allows `s3:GetObject` with a condition on `aws:PrincipalOrgID`
- C. Create an IAM user in the bucket's account for each team, and share the credentials
- D. List every account ID in the bucket policy, and update it for each new account

> [!success]- Answer
> **B.** `aws:PrincipalOrgID` matches any principal in the organisation, so new accounts work automatically. Listing accounts needs constant updates. Shared IAM users are poor practice. A public bucket exposes the data to everyone.
>
> *Task 1.1.* Review: [[02 IAM and Federation#Useful condition keys|Useful condition keys]]

**62.** A reporting database is needed for one week each quarter. It sits idle the rest of the time. What is the most cost-effective approach?

- A. Buy a three-year Reserved Instance
- B. Take a snapshot and delete the database, then restore it when needed
- C. Enable Multi-AZ
- D. Stop the database between uses

> [!success]- Answer
> **B.** Snapshots cost much less than a running database. A stopped database still bills for storage, and it restarts after seven days. An RI pays for idle time. Multi-AZ adds cost.
>
> *Task 4.3.* Review: [[13 RDS and Aurora#Backups and restore|Backups and restore]]

**63.** A company serves popular large files from S3 directly to users worldwide, and it pays high data transfer charges. Requests are read-only. What is the most effective change?

- A. Enable S3 Transfer Acceleration
- B. Move the files to S3 One Zone-IA
- C. Replicate the files to a second Region
- D. Serve the files through Amazon CloudFront

> [!success]- Answer
> **D.** CloudFront caches at the edge, and transfer from S3 to CloudFront is free. One Zone-IA changes storage only. Transfer Acceleration adds cost and is mostly for uploads. A second Region adds cost.
>
> *Task 4.1.* Review: [[12 CloudFront and Global Accelerator#Caching|Caching]]

**64.** A loan application must be validated, sent to a credit check service, wait up to five days for a human approver, and then notify the customer. The team wants built-in retries and a record of each step. What should a solutions architect use?

- A. AWS Step Functions Express workflow
- B. AWS Step Functions Standard workflow with a callback task for the approval
- C. An SQS delay queue to wait for the approval
- D. A chain of Lambda functions that sleep while waiting

> [!success]- Answer
> **B.** Standard workflows run for up to a year and record each step. Express workflows stop at five minutes and do not support callbacks. SQS delays are limited to 15 minutes. Lambda stops at 15 minutes.
>
> *Task 2.1.* Review: [[20 Messaging and Integration#AWS Step Functions|AWS Step Functions]]

**65.** A three-tier application has web servers behind an ALB, application servers in an Auto Scaling group, and an RDS for MySQL database. All application servers and the database are in private subnets. Instance IP addresses change as the group scales. Only the application tier may connect to the database. What should a solutions architect configure?

- A. Add a deny rule for the web tier to the database security group
- B. Allow port 3306 from 0.0.0.0/0 on the database, and rely on the private subnet
- C. Add an inbound rule on the database security group for port 3306, with the application tier's security group as the source
- D. Add inbound rules to the network ACL for each application server's IP address

> [!success]- Answer
> **C.** A security group reference keeps working as instances change. A NACL has no awareness of instances and would need constant updates. An open rule allows anything in the VPC to connect. Security groups have no deny rules.
>
> *Task 1.2.* Review: [[09 VPC Fundamentals#Security groups|Security groups]]

## Score your exam

Mark your answers with the key, then count your correct answers for each domain.

> [!example]- Answer key
> 1: C · 2: C · 3: A · 4: C · 5: D · 6: C · 7: B · 8: D · 9: C · 10: D  
> 11: B · 12: A · 13: A · 14: A, B · 15: D · 16: C · 17: A · 18: D · 19: D · 20: D  
> 21: B · 22: C · 23: B · 24: D · 25: C · 26: C · 27: A · 28: B · 29: C · 30: A  
> 31: D · 32: A · 33: C · 34: B · 35: C · 36: C, D · 37: D · 38: A · 39: A, D · 40: A  
> 41: B, E · 42: C · 43: A · 44: D · 45: C · 46: A · 47: D · 48: A · 49: D · 50: A, E  
> 51: D · 52: D · 53: C · 54: B · 55: D · 56: C · 57: C · 58: B · 59: A · 60: A  
> 61: B · 62: B · 63: D · 64: B · 65: C  

| Domain | Questions | Your score |
| --- | --- | --- |
| Domain 1: Secure | 2, 5, 14, 15, 18, 22, 28, 29, 30, 31, 32, 34, 36, 38, 44, 45, 47, 56, 61, 65 | ___ / 20 |
| Domain 2: Resilient | 3, 4, 6, 7, 8, 9, 12, 13, 24, 27, 39, 43, 53, 55, 58, 60, 64 | ___ / 17 |
| Domain 3: High-Performing | 11, 16, 17, 19, 23, 25, 26, 37, 41, 46, 50, 51, 52, 54, 57 | ___ / 15 |
| Domain 4: Cost-Optimized | 1, 10, 20, 21, 33, 35, 40, 42, 48, 49, 59, 62, 63 | ___ / 13 |
| **Total** | | **___ / 65** |

Add your result to the table in the [[Study Guide#Tracking your progress|Study Guide]], and every mistake to the [[Mistake Log]].

---
**Next:** [[Practice Exam 2]] · **Plan:** [[Study Guide]]
