---
tags: [practice, scope/in]
---

# Practice Exam 3

> [!info] How to sit this exam
> - Set a timer for **130 minutes**, and sit it in one go, with no notes.
> - Write your answers on paper or in another note, and do not open the answers until you finish.
> - There are 65 questions. The real exam has 15 unscored questions, but all of these count here.
> - Score it with the table at the end, then review every question.
> - Aim for **80% or more** (52 of 65). See the [[Study Guide#Step 12 The readiness gate|readiness gate]].
>
> These are original practice questions written for this vault. They are not real exam questions, their difficulty has not been calibrated against the real exam, and real questions are often longer, so expect to do more reading on the day.

**1.** A latency-sensitive application serves users in one large city far from any AWS Region. What is the best way to place compute close to them?

- A. Use an AWS Local Zone in that city
- B. Use the nearest Region with larger instances
- C. Use AWS Wavelength with no telecom partner
- D. Use AWS Outposts in a user's home

> [!success]- Answer
> **A.** Local Zones extend a Region into a metro area. Bigger instances do not cut network distance. Wavelength is for 5G networks through a carrier. Outposts go in your own data centre.
>
> *Task 3.4.* Review: [[01 Cloud Foundations#Choosing a Region|Choosing a Region]]

**2.** A service calls a downstream API that sometimes throttles. Under load, all clients retry at once, and the problem gets worse. Which change should a solutions architect recommend?

- A. Retry with exponential backoff and jitter
- B. Add more retries with no delay
- C. Remove the timeout on the client
- D. Retry immediately in a tight loop

> [!success]- Answer
> **A.** Backoff with jitter spreads out retries. Immediate retries make throttling worse. Removing timeouts leaves clients hanging.
>
> *Task 2.2.* Review: [[28 High Availability and Disaster Recovery#Distributed design patterns|Distributed design patterns]]

**3.** A global application uses client-side encryption, and data encrypted in us-east-1 must be decrypted in eu-west-1 without a cross-Region API call. Which feature fits?

- A. A single KMS key shared across Regions with a key policy
- B. S3 Bucket Keys
- C. AWS KMS Multi-Region keys
- D. AWS managed keys

> [!success]- Answer
> **C.** Multi-Region keys have the same material and key ID in each Region. A normal KMS key lives in one Region. Bucket Keys only reduce KMS calls for S3. AWS managed keys cannot be used this way.
>
> *Task 1.3.* Review: [[23 Encryption and Secrets#Regional scope|Regional scope]]

**4.** A regulation requires two independent layers of encryption for data in S3, using keys managed in AWS KMS. Which option meets it?

- A. SSE-C
- B. SSE-S3
- C. SSE-KMS with a Bucket Key
- D. DSSE-KMS

> [!success]- Answer
> **D.** DSSE-KMS applies two layers. The others apply one layer of server-side encryption.
>
> *Task 1.3.* Review: [[07 S3 Security and Data Protection#Encryption at rest|Encryption at rest]]

**5.** GuardDuty raised a finding about unusual API calls by a role. An analyst needs to explore related activity, across CloudTrail and VPC Flow Logs, to find how it began. Which service is designed for this?

- A. Amazon Detective
- B. AWS Config
- C. AWS Artifact
- D. Amazon Inspector

> [!success]- Answer
> **A.** Detective builds a graph from these sources to help find root causes. Inspector scans for vulnerabilities. Artifact provides compliance reports. Config records configuration.
>
> *Task 1.2.* Review: [[24 Threat Protection and Security Services#Amazon Detective|Amazon Detective]]

**6.** A company's on-premises block storage is running out of space. It wants most data in AWS, and frequently used data held locally with low latency. Applications use iSCSI. Which solution fits?

- A. S3 File Gateway
- B. Tape Gateway
- C. Volume Gateway in cached mode
- D. Volume Gateway in stored mode

> [!success]- Answer
> **C.** Cached mode keeps primary data in AWS, with a local cache. Stored mode keeps all data local. File Gateway uses NFS or SMB. Tape Gateway is for backups.
>
> *Task 3.1.* Review: [[27 Migration and Data Transfer#AWS Storage Gateway|AWS Storage Gateway]]

**7.** When an item in a DynamoDB table changes, a search index and an audit log must both be updated, and failures must not affect the writers. What is the best design?

- A. Enable DynamoDB Streams, and process changes with Lambda
- B. Poll the table every minute with a scan
- C. Have the application write to all three systems synchronously
- D. Use DAX to forward changes

> [!success]- Answer
> **A.** Streams decouple writers from consumers. Synchronous writes couple them, so that one failure affects all. Scans are costly and slow. DAX is a cache.
>
> *Task 2.1.* Review: [[14 DynamoDB#DynamoDB Streams|DynamoDB Streams]]

**8.** Static content is served from S3 through CloudFront. If the primary bucket's Region has problems, viewers should get content from a replica bucket in another Region. Which solution fits?

- A. Use two distributions, and ask users to switch
- B. Configure an origin group with the two buckets, and S3 Cross-Region Replication between them
- C. Use a Network Load Balancer in front of S3
- D. Use S3 Transfer Acceleration

> [!success]- Answer
> **B.** Origin failover retries the second bucket, and replication keeps it current. An NLB cannot target S3. Transfer Acceleration is for uploads.
>
> *Task 2.2.* Review: [[12 CloudFront and Global Accelerator#Availability|Availability]]

**9.** An internal web application behind an ALB must require employees to sign in through the company's OIDC identity provider. The application should need no code changes. What should a solutions architect do?

- A. Use a Network Load Balancer with TLS passthrough
- B. Add a Lambda authoriser to the ALB
- C. Add a CloudFront signed cookie to each request
- D. Configure an authenticate-oidc action on the ALB listener rule

> [!success]- Answer
> **D.** ALBs can authenticate users through OIDC or Cognito before forwarding the request. Lambda authorisers belong to API Gateway. Signed cookies do not sign users in. An NLB does not look at HTTP.
>
> *Task 1.2.* Review: [[05 Load Balancing and Auto Scaling#Application Load Balancer|Application Load Balancer]]

**10.** An application needs very high random read and write performance on a local NVMe disk, and it replicates data between nodes itself. Which instance family is best?

- A. R family
- B. T family
- C. P family
- D. I family

> [!success]- Answer
> **D.** I instances offer fast local NVMe storage. T is burstable, R is memory optimised, and P is for GPU training.
>
> *Task 3.2.* Review: [[04 Amazon EC2#Instance types|Instance types]]

**11.** A bucket must accept requests only from instances in one VPC. The instances use an S3 gateway endpoint. Which combination enforces this? (Choose two.)

- A. A bucket policy that denies requests unless `aws:SourceVpce` matches the endpoint
- B. A network ACL on the bucket
- C. A security group on the bucket
- D. A NAT gateway route for S3 traffic
- E. An endpoint policy that limits which buckets can be reached through the endpoint

> [!success]- Answer
> **A and E.** The bucket policy restricts who can reach the bucket, and the endpoint policy restricts what can be reached from the VPC. Buckets are not in subnets, so NACLs and security groups do not apply. NAT would bypass the endpoint.
>
> *Task 1.2.* Review: [[10 VPC Connectivity and Hybrid Networking#VPC endpoints|VPC endpoints]]

**12.** A company wants the lowest-cost way to archive 30 TB from a site with a 50 Mbps link into S3 Glacier Deep Archive, within two weeks. It is an existing Snowball customer. What should it do?

- A. Upload directly over the 50 Mbps link
- B. Use Snowball Edge to import to S3, then a lifecycle rule to move the objects to Deep Archive
- C. Use a Snowball Edge to write straight to Deep Archive
- D. Set up Direct Connect at 10 Gbps

> [!success]- Answer
> **B.** The link would take about 55 days. Snowball imports into S3 first, and a lifecycle rule handles the rest. Direct Connect is unlikely to arrive in time.
>
> *Task 4.1.* Review: [[27 Migration and Data Transfer#AWS Snow Family|AWS Snow Family]]

**13.** A company has billions of existing unencrypted objects in S3, from before default encryption began, and it needs them encrypted with SSE-KMS. Which is the most efficient way to do this?

- A. Use S3 Batch Operations to copy the objects in place with the new encryption setting
- B. Download and upload each object with a script on EC2
- C. Enable S3 Versioning
- D. Enable default bucket encryption, which converts them

> [!success]- Answer
> **A.** Batch Operations handles this at scale, with retries and reporting. Default encryption affects only new objects. A script is slow and fragile. Versioning does not encrypt anything.
>
> *Task 1.3.* Review: [[07 S3 Security and Data Protection#Encryption at rest|Encryption at rest]]

**14.** A company's EC2 instances in a VPC call AWS Systems Manager and CloudWatch through a NAT gateway, and the NAT processing charges are high. What is a good way to reduce them?

- A. Create interface VPC endpoints for these services
- B. Add a second NAT gateway in the same AZ
- C. Create gateway endpoints for these services
- D. Move the instances to a public subnet with public IPs

> [!success]- Answer
> **A.** Interface endpoints avoid NAT for these services, and can be cheaper at high volumes. Gateway endpoints support only S3 and DynamoDB.
>
> *Task 4.4.* Review: [[29 Cost Optimisation#Network costs|Network costs]]

**15.** A nightly Glue job reprocesses the same files in S3 each time, which wastes money. What is the simplest way to process only new data?

- A. Use S3 Versioning
- B. Enable Glue job bookmarks
- C. Use Athena workgroups
- D. Use a larger worker type

> [!success]- Answer
> **B.** Bookmarks track what has been processed. Larger workers cost more. Versioning does not track processing.
>
> *Task 3.5.* Review: [[22 Data Lakes and Analytics#AWS Glue|AWS Glue]]

**16.** A machine learning application must read billions of small objects from S3, with single-digit millisecond latency, and it runs in one AZ. Which option fits?

- A. S3 Express One Zone in a directory bucket in the same AZ
- B. S3 Glacier Instant Retrieval
- C. S3 Intelligent-Tiering
- D. S3 Standard-IA

> [!success]- Answer
> **A.** Express One Zone is built for this latency. The other classes are normal S3 latency, and Glacier Instant and IA add retrieval fees.
>
> *Task 3.1.* Review: [[06 Amazon S3#Performance|Performance]]

**17.** A test environment runs on 20 instances for office hours only, Monday to Friday. Instances take a long time to initialise. Which combination is most cost-effective?

- A. Keep them running with Compute Savings Plans
- B. Buy three-year Reserved Instances
- C. Move them to Dedicated Instances
- D. Stop or hibernate the instances out of hours, on a schedule

> [!success]- Answer
> **D.** Not running the instances out of hours removes most of the cost, and hibernation avoids the slow start. Commitments pay for idle time.
>
> *Task 4.2.* Review: [[29 Cost Optimisation#Compute costs|Compute costs]]

**18.** A company wants to find IAM roles and S3 buckets that can be reached from outside its organisation, and it also wants to spot unused permissions so that it can remove them. Which service covers both?

- A. AWS Trusted Advisor
- B. Amazon Macie
- C. Amazon Inspector
- D. IAM Access Analyzer

> [!success]- Answer
> **D.** Access Analyzer reports external access and unused access. Inspector looks for vulnerabilities. Trusted Advisor gives general checks. Macie finds sensitive data.
>
> *Task 1.1.* Review: [[02 IAM and Federation#Auditing IAM|Auditing IAM]]

**19.** A company wants to make sure that no VPC in an account has internet access, whatever the route tables or gateways say, while it reviews its network design. Which feature fits best?

- A. A network ACL on each subnet
- B. An IAM policy that denies `ec2:*`
- C. Removing the Elastic IP addresses
- D. VPC Block Public Access

> [!success]- Answer
> **D.** VPC Block Public Access blocks internet traffic across VPCs in a single setting. NACLs need managing per subnet. Removing Elastic IPs misses other public addresses. An IAM policy does not affect network traffic.
>
> *Task 1.2.* Review: [[09 VPC Fundamentals#Other tools|Other tools]]

**20.** A company wants one place to set scaling targets for its EC2 Auto Scaling groups, ECS services, DynamoDB tables and Aurora replicas. Which service fits?

- A. AWS Compute Optimizer
- B. AWS Auto Scaling
- C. AWS Trusted Advisor
- D. Amazon EC2 Auto Scaling only

> [!success]- Answer
> **B.** AWS Auto Scaling covers scaling plans across these resources. EC2 Auto Scaling covers only EC2. The others give recommendations.
>
> *Task 2.1.* Review: [[05 Load Balancing and Auto Scaling#AWS Auto Scaling and Application Auto Scaling|AWS Auto Scaling and Application Auto Scaling]]

**21.** A company runs Kubernetes on-premises with Helm charts and custom controllers, and it wants to move to AWS with as few changes as possible, without managing the control plane. What should it use?

- A. Amazon ECS with Fargate
- B. Amazon EKS with managed node groups
- C. Kubernetes installed on EC2 by hand
- D. AWS Elastic Beanstalk with Docker

> [!success]- Answer
> **B.** EKS keeps Kubernetes tools, and AWS manages the control plane. ECS and Beanstalk would need a redesign. Self-managed Kubernetes keeps the control plane work.
>
> *Task 2.1.* Review: [[18 Containers#Amazon EKS|Amazon EKS]]

**22.** A Linux file share on EFS holds many files that are not touched for months. Which option lowers cost with the least work?

- A. Add a lifecycle policy to move files to EFS Infrequent Access and Archive
- B. Move all the files to instance store
- C. Move all the files to EBS gp3
- D. Change the performance mode to Max I/O

> [!success]- Answer
> **A.** Lifecycle policies tier files automatically. EBS cannot be shared in the same way. Instance store is temporary. Max I/O is a previous-generation mode, and it does not save money.
>
> *Task 4.1.* Review: [[08 Block and File Storage#Types, classes and modes|Types, classes and modes]]

**23.** An Aurora cluster has large replicas for analytics and small ones for the application. Analytics queries must run only on the large replicas. What should a solutions architect create?

- A. A second writer endpoint
- B. A read replica in another Region
- C. A custom endpoint that includes the large replicas
- D. A Route 53 weighted record

> [!success]- Answer
> **C.** Custom endpoints direct connections to a chosen set of instances. Aurora has one writer endpoint. DNS routing is not aware of instance roles.
>
> *Task 3.3.* Review: [[13 RDS and Aurora#Endpoints|Endpoints]]

**24.** A legacy licence server must run on exactly one EC2 instance, and it depends on keeping its private IP. If the underlying host fails, it should come back automatically. What is the simplest solution?

- A. Use EC2 automatic recovery, with a CloudWatch alarm or the default recovery behaviour
- B. Deploy two instances behind an ALB
- C. Put it in a Spot Fleet
- D. Use a cluster placement group

> [!success]- Answer
> **A.** Recovery moves the instance to healthy hardware and keeps its private IP. A Spot Fleet can be interrupted. Two instances break the single-instance requirement.
>
> *Task 2.2.* Review: [[04 Amazon EC2#Status checks and recovery|Status checks and recovery]]

**25.** A team stores objects that are read rarely, and each is deleted after 15 days. Someone suggests Standard-IA to save money. What is the likely result?

- A. It is not possible to delete objects in Standard-IA
- B. It will not save money, because Standard-IA bills a minimum of 30 days
- C. It will save money, because retrieval is free
- D. It will save money, because storage is cheaper

> [!success]- Answer
> **B.** The 30-day minimum means that each object is charged for twice as long as it exists, plus retrieval fees.
>
> *Task 4.1.* Review: [[06 Amazon S3#Storage classes|Storage classes]]

**26.** A company has 80 accounts, and it wants the same WAF rules and security group baselines applied to all of them. New accounts must get these automatically. Which service should it use?

- A. AWS Config rules with email alerts
- B. AWS Firewall Manager with AWS Organizations
- C. AWS Shield Standard
- D. AWS RAM

> [!success]- Answer
> **B.** Firewall Manager applies these policies across the organisation, and includes new accounts. Shield Standard has no such rules. Config alerts only. RAM shares resources.
>
> *Task 1.2.* Review: [[24 Threat Protection and Security Services#AWS Firewall Manager|AWS Firewall Manager]]

**27.** A team has a small order API that sends confirmation emails to customers, and it wants to send these from a Lambda function without managing mail servers. Which service is the natural fit?

- A. Amazon Kinesis
- B. Amazon SES
- C. AWS AppFlow
- D. Amazon SQS

> [!success]- Answer
> **B.** SES sends email at scale. The others are not email services.
>
> *Task 2.1.* Review: [[20 Messaging and Integration#Other integration services|Other integration services]]

**28.** A web application on Elastic Beanstalk has long-running jobs, such as PDF generation, which slow down user requests. Which design decouples them with the least change?

- A. Move the jobs to a Beanstalk web server tier with sticky sessions
- B. Increase the web instances' size
- C. Add a worker environment that processes jobs from an SQS queue
- D. Run the jobs in CloudFront Functions

> [!success]- Answer
> **C.** The worker tier takes jobs from SQS, away from user requests. Bigger instances only delay the issue. CloudFront Functions run for under a millisecond.
>
> *Task 2.1.* Review: [[19 Other Compute Services#Good practice|Good practice]]

**29.** A company must send all traffic entering its VPCs through a fleet of third-party next-generation firewall appliances, and it must be able to scale the appliances without changing routes. Which solution fits?

- A. Use AWS WAF to forward traffic to the appliances
- B. Deploy the appliances behind an Application Load Balancer
- C. Deploy the appliances behind a Gateway Load Balancer, and route traffic through Gateway Load Balancer endpoints
- D. Deploy the appliances behind a Network Load Balancer with TLS listeners

> [!success]- Answer
> **C.** GWLB is built for transparent appliance fleets, using GENEVE on port 6081. ALB and NLB terminate or forward at higher layers and are not transparent. WAF filters web requests, and it does not forward traffic to appliances.
>
> *Task 1.2.* Review: [[05 Load Balancing and Auto Scaling#Gateway Load Balancer|Gateway Load Balancer]]

**30.** Auditors want proof that CloudTrail log files in S3 were not modified after delivery, and they must be kept for seven years in a way that cannot be deleted. Which combination fits? (Choose two.)

- A. Use the CloudTrail event history
- B. Use S3 Object Lock in Compliance mode on the log bucket
- C. Enable S3 Transfer Acceleration
- D. Turn on Amazon Macie
- E. Enable CloudTrail log file integrity validation

> [!success]- Answer
> **B and E.** Integrity validation proves that files are unchanged, and Object Lock protects them from deletion. Event history lasts 90 days. The other options do not address this need.
>
> *Task 1.3.* Review: [[25 Monitoring and Auditing#AWS CloudTrail|AWS CloudTrail]]

**31.** A company runs fault-tolerant batch containers on ECS Fargate, and it wants to lower compute costs without changing the application. Which option fits?

- A. Use Dedicated Hosts
- B. Move to EKS on Fargate with Spot
- C. Use Fargate Spot for these tasks
- D. Move to larger task sizes

> [!success]- Answer
> **C.** Fargate Spot is discounted for interruptible tasks. Dedicated Hosts cost more. EKS on Fargate does not support Fargate Spot.
>
> *Task 4.2.* Review: [[18 Containers#AWS Fargate|AWS Fargate]]

**32.** A website must validate a JWT at the edge by calling an external key service before serving content. Which feature fits?

- A. S3 presigned URLs
- B. Lambda@Edge
- C. A Route 53 health check
- D. CloudFront Functions

> [!success]- Answer
> **B.** Lambda@Edge allows network calls. CloudFront Functions cannot make them. The others do not run logic at the edge.
>
> *Task 3.4.* Review: [[12 CloudFront and Global Accelerator#Edge functions|Edge functions]]

**33.** A company wants to lower EC2 costs and improve energy efficiency for a stateless web application compiled for multiple architectures. Which change fits?

- A. Use the same instances on a shorter monitoring period
- B. Move to G family instances
- C. Move to Graviton-based instances
- D. Move to Dedicated Hosts

> [!success]- Answer
> **C.** Graviton gives better price-performance. Dedicated Hosts cost more. G instances are for graphics.
>
> *Task 4.2.* Review: [[04 Amazon EC2#Instance types|Instance types]]

**34.** A penetration test showed that a server-side request forgery flaw in a web application could read the instance's temporary credentials. Which change directly reduces this risk?

- A. Disable the instance's public IP
- B. Attach a larger instance profile policy
- C. Move the instances to a private subnet
- D. Require IMDSv2 on the instances

> [!success]- Answer
> **D.** IMDSv2 needs a session token, which blocks simple SSRF attacks on the metadata service. The flaw is exploited through the application, so moving subnets does not stop it.
>
> *Task 1.2.* Review: [[04 Amazon EC2#User data and instance metadata|User data and instance metadata]]

**35.** A company has hundreds of projects, each with its own developers and resources, and new projects start every week. Writing a new IAM policy for each project has become unmanageable. Developers should reach only resources tagged with their own project. What should a solutions architect recommend?

- A. Role-based access control, with a new role for each project
- B. An IAM group for each project, with an inline policy listing resource ARNs
- C. A separate VPC for each project, with security groups limiting access
- D. Attribute-based access control, with a single policy that compares `aws:PrincipalTag/Project` with `aws:ResourceTag/Project`

> [!success]- Answer
> **D.** ABAC uses one policy that keeps working as projects are added, because access follows tags. A role or group per project is the unmanageable approach being described. VPCs control network traffic, not API access.
>
> *Task 1.1.* Review: [[02 IAM and Federation#Least privilege|Least privilege]]

**36.** An EKS cluster needs to add well-fitted nodes quickly when pods cannot be scheduled, across many instance types. Which option should a solutions architect recommend?

- A. EC2 Reserved Instances
- B. An Application Load Balancer
- C. Horizontal Pod Autoscaler alone
- D. Karpenter

> [!success]- Answer
> **D.** Karpenter launches suitable nodes quickly. HPA scales pods and not nodes. The others do not add capacity.
>
> *Task 3.2.* Review: [[18 Containers#Scaling|Scaling]]

**37.** Workers process SQS messages, and each job normally takes 2 minutes, but some take 20 minutes. Setting the visibility timeout to 20 minutes for everything delays retries after a crash. What is the best approach?

- A. Set the timeout to 12 hours
- B. Set the timeout to 0 seconds
- C. Move to SNS, which has no visibility timeout
- D. Keep a moderate visibility timeout, and have workers call `ChangeMessageVisibility` to extend it while they work

> [!success]- Answer
> **D.** Workers can extend the timeout only when needed, so crashes are still retried quickly. A very long timeout delays recovery. Zero seconds causes duplicates. SNS does not queue work.
>
> *Task 2.1.* Review: [[20 Messaging and Integration#Visibility timeout|Visibility timeout]]

**38.** A batch job runs for up to eight hours and uses an IAM role that it assumes through `sts:AssumeRole`. It fails after one hour with an expired token error. What is the simplest fix?

- A. Create an IAM user for the job, and store its access keys
- B. Attach an inline policy with `sts:*`
- C. Increase the role's maximum session duration, and request a longer session when assuming it
- D. Move the job to a Lambda function

> [!success]- Answer
> **C.** Sessions last one hour by default, and a role can be configured for up to 12 hours. Long-lived keys are the wrong pattern. Extra STS permissions do not extend a session. Lambda stops at 15 minutes.
>
> *Task 1.1.* Review: [[02 IAM and Federation#Roles and temporary credentials|Roles and temporary credentials]]

**39.** A Java Lambda function behind API Gateway has slow cold starts. The team wants faster start-up at no extra cost. Which feature fits?

- A. Lambda SnapStart
- B. A larger `/tmp`
- C. Reserved concurrency
- D. Provisioned concurrency

> [!success]- Answer
> **A.** SnapStart restores from a snapshot, and it is free for Java. Provisioned concurrency also works, but it costs extra. Reserved concurrency does not remove cold starts.
>
> *Task 3.2.* Review: [[16 Lambda and Serverless#Cold starts and concurrency|Cold starts and concurrency]]

**40.** An Aurora cluster's bill shows that I/O charges are about 40% of its total cost. What should a solutions architect recommend?

- A. Switch the cluster to Aurora I/O-Optimized
- B. Enable Backtrack
- C. Switch to Aurora Standard
- D. Add read replicas

> [!success]- Answer
> **A.** I/O-Optimized suits clusters where I/O is 25% or more of spending. Standard charges per I/O. Backtrack and replicas do not lower I/O charges.
>
> *Task 4.3.* Review: [[13 RDS and Aurora#Storage configurations|Storage configurations]]

**41.** A company has 60 VPCs that exchange small amounts of data with each other, and a growing number of peering links has become hard to manage. Which option reduces the management work, knowing that it costs more per GB?

- A. AWS PrivateLink for all traffic
- B. Public internet with TLS
- C. AWS Transit Gateway
- D. More VPC peering connections

> [!success]- Answer
> **C.** Transit Gateway centralises routing. Peering scales poorly. PrivateLink exposes single services. The internet does not simplify management.
>
> *Task 4.4.* Review: [[29 Cost Optimisation#Connection choices|Connection choices]]

**42.** A company with a single AWS account uses a SAML 2.0 identity provider. It wants employees to sign in to the console with their corporate credentials, with no user objects in AWS. It does not plan to add more accounts. Which approach is the most direct?

- A. Create a Cognito user pool, and put it in front of the console
- B. Create an IAM user for each employee, and sync passwords nightly
- C. Install Simple AD, and join each laptop to it
- D. Create a SAML identity provider in IAM, with roles that employees assume through `AssumeRoleWithSAML`

> [!success]- Answer
> **D.** IAM SAML federation fits a single account. Identity Center would also work and is generally preferred, but it is not offered here. Cognito is for customers of an application. IAM users are what the company wants to avoid. Simple AD is closed to new customers.
>
> *Task 1.1.* Review: [[02 IAM and Federation#Federation|Federation]]

**43.** A Redis OSS cache holds more data than fits on a single node, and write traffic is growing. Which ElastiCache option fits?

- A. Cluster mode enabled, with several shards
- B. Cluster mode disabled, with more replicas
- C. Memcached with read replicas
- D. A single larger node with AOF

> [!success]- Answer
> **A.** Cluster mode partitions data across shards, which scales writes and memory. More replicas scale only reads. Memcached has no replicas.
>
> *Task 3.3.* Review: [[15 ElastiCache and Other Databases#Cluster modes|Cluster modes]]

**44.** A company runs Kafka Connect and many Kafka consumers on EC2, and it wants to reduce operations without changing client code. Which service fits?

- A. Amazon Data Firehose
- B. Amazon SQS
- C. AWS Glue
- D. Amazon MSK

> [!success]- Answer
> **D.** MSK runs Apache Kafka with the same API. The others would mean a rewrite.
>
> *Task 3.5.* Review: [[21 Streaming and Data Ingestion#Amazon MSK|Amazon MSK]]

**45.** A company has Linux and Windows clients that must access the same data with NFS and SMB, and it wants point-in-time clones for testing and automatic tiering of cold data. Which service fits?

- A. Amazon FSx for Windows File Server
- B. Amazon EFS
- C. Amazon FSx for NetApp ONTAP
- D. Amazon FSx for Lustre

> [!success]- Answer
> **C.** ONTAP supports both protocols, clones and tiering. EFS is NFS only. Lustre is for HPC on Linux. FSx for Windows is SMB-focused.
>
> *Task 3.1.* Review: [[08 Block and File Storage#FSx for NetApp ONTAP|FSx for NetApp ONTAP]]

**46.** A company uploads 100 million very small records a day to S3 as individual objects, and PUT request charges are high. What is the best way to reduce them?

- A. Move to S3 Standard-IA
- B. Add more prefixes
- C. Enable Transfer Acceleration
- D. Batch records into larger files before uploading

> [!success]- Answer
> **D.** S3 charges per request, so fewer, larger objects cost less. Standard-IA has a higher request price and a 128 KB minimum. The other options add no saving.
>
> *Task 4.1.* Review: [[29 Cost Optimisation#Storage costs|Storage costs]]

**47.** Ransomware protection is a board priority. Backups must stay recoverable even if the production account is fully compromised. What is the strongest design?

- A. Export the backups to a second bucket in the same account
- B. Use EBS snapshots in the same account with tags
- C. Copy backups with AWS Backup to a vault in a separate account, with Vault Lock in compliance mode
- D. Keep all backups in the production account with IAM restrictions

> [!success]- Answer
> **C.** A separate account plus a locked vault removes the single compromised boundary. Anything in the production account can be deleted by someone with full control of it.
>
> *Task 1.3.* Review: [[28 High Availability and Disaster Recovery#AWS Backup|AWS Backup]]

**48.** A company runs SQL Server on RDS with Windows Authentication, and it wants on-premises users to log in with their existing accounts. Which approach should a solutions architect use?

- A. Simple AD with a one-way trust
- B. A Cognito user pool with SAML
- C. AWS Managed Microsoft AD, joined to RDS, with a trust to the on-premises domain
- D. AD Connector only

> [!success]- Answer
> **C.** RDS for SQL Server integrates with AWS Managed Microsoft AD, and a trust brings in on-premises users. Simple AD does not support trusts, and Cognito is not a Windows directory.
>
> *Task 1.1.* Review: [[02 IAM and Federation#AWS Directory Service|AWS Directory Service]]

**49.** Business analysts run complex joins across a Redshift warehouse, and also need to include several years of older data in S3 without loading it. Which feature should they use?

- A. Redshift Spectrum
- B. S3 Select
- C. Redshift Concurrency Scaling
- D. Athena workgroups only

> [!success]- Answer
> **A.** Spectrum queries S3 data from Redshift. Concurrency Scaling handles bursts. S3 Select is closed to new customers.
>
> *Task 3.5.* Review: [[22 Data Lakes and Analytics#Amazon Redshift|Amazon Redshift]]

**50.** A company runs Aurora, RDS and DynamoDB steadily across two Regions, and it expects to change engines during the next year. Which option is the most flexible way to get a discount?

- A. Database Savings Plans
- B. Spot Instances
- C. EC2 Instance Savings Plans
- D. Standard Reserved Instances for each database

> [!success]- Answer
> **A.** Database Savings Plans apply across engines and Regions. RIs are tied to a configuration. EC2 Instance Savings Plans do not cover databases. Spot is not for databases.
>
> *Task 4.3.* Review: [[04 Amazon EC2#Savings Plans|Savings Plans]]

**51.** A company runs 200 on-premises servers and wants a low-cost DR site in AWS, with an RPO of seconds and recovery in minutes. It does not want to pay for running servers in AWS until a disaster. Which service fits?

- A. AWS Elastic Disaster Recovery
- B. AWS Storage Gateway Tape Gateway
- C. AWS DataSync
- D. AWS Application Discovery Service

> [!success]- Answer
> **A.** DRS keeps servers replicated to low-cost staging and launches them on demand. DataSync moves files. Discovery plans migrations. Tape Gateway handles backups.
>
> *Task 2.2.* Review: [[28 High Availability and Disaster Recovery#AWS Elastic Disaster Recovery|AWS Elastic Disaster Recovery]]

**52.** An Aurora cluster has a writer and three replicas of different sizes. The team wants a specific large replica to become the writer on failover. What should it set?

- A. A failover priority tier on the replica
- B. A larger storage volume
- C. A custom endpoint for the replica
- D. A Route 53 failover record

> [!success]- Answer
> **A.** Failover priority tiers control which replica is promoted. A custom endpoint groups instances for connections. Aurora storage is shared.
>
> *Task 2.2.* Review: [[13 RDS and Aurora#Architecture|Architecture]]

**53.** A central networking team wants application teams in other accounts to launch resources into subnets it manages, without peering and without giving those teams the ability to change the VPC. Which solution fits?

- A. Use AWS PrivateLink for each application
- B. Create VPC peering between the accounts, and let teams create subnets
- C. Give application teams an IAM role in the networking account
- D. Share the subnets from the owner account using AWS RAM

> [!success]- Answer
> **D.** VPC sharing through RAM lets participants launch into subnets, and they cannot change the VPC. Peering connects separate VPCs. A role in the networking account gives too much access. PrivateLink exposes individual services.
>
> *Task 1.1.* Review: [[03 Multi-Account Governance#AWS Resource Access Manager|AWS Resource Access Manager]]

**54.** A Lambda function is invoked asynchronously by S3. Failures must be captured for later analysis, with the event details and error information. What should a solutions architect configure?

- A. Reserved concurrency
- B. Lambda SnapStart
- C. An on-failure destination, such as an SQS queue or EventBridge
- D. A longer function timeout

> [!success]- Answer
> **C.** On-failure destinations keep the event and the error details. Reserved concurrency controls scaling. A longer timeout does not capture failures. SnapStart is about start-up time.
>
> *Task 2.1.* Review: [[16 Lambda and Serverless#How functions are invoked|How functions are invoked]]

**55.** A DynamoDB table sees throttling on a small number of very popular items, even though total capacity is not reached. Which two actions could help? (Choose two.)

- A. Choose a partition key with higher cardinality, or add a suffix to spread writes
- B. Reduce the item size limit
- C. Add DAX to absorb repeated reads of popular items
- D. Turn on TTL
- E. Add an LSI

> [!success]- Answer
> **A and C.** A better key spreads traffic, and DAX absorbs hot reads. An LSI does not spread partition traffic. TTL only deletes old items.
>
> *Task 3.3.* Review: [[14 DynamoDB#Data model|Data model]]

**56.** A security team attached an SCP that denies `s3:DeleteBucket` to all member accounts. A support engineer points out that an AWS service, working on behalf of an account, can still perform some actions that the SCP denies. What is the most likely explanation?

- A. SCPs apply only to the root user
- B. SCPs do not affect service-linked roles
- C. SCPs do not apply to any IAM roles
- D. SCPs take effect only after 24 hours

> [!success]- Answer
> **B.** Service-linked roles are not affected by SCPs. All other users and roles in member accounts are, including the root user of those accounts.
>
> *Task 1.1.* Review: [[03 Multi-Account Governance#Service control policies|Service control policies]]

**57.** A nightly job must process five million objects in S3 in parallel, with limited concurrency, and error handling for each item. The company wants no servers to manage. Which solution fits best?

- A. AWS Step Functions with a Map state in Distributed mode
- B. One Lambda function that loops through all the objects
- C. A single EC2 instance running a script
- D. An SNS topic with a subscriber for each object

> [!success]- Answer
> **A.** Distributed Map runs large parallel jobs as child executions, with concurrency limits. A single function stops at 15 minutes. EC2 means servers to manage. SNS does not orchestrate work.
>
> *Task 2.1.* Review: [[20 Messaging and Integration#AWS Step Functions|AWS Step Functions]]

**58.** A company collects billions of sensor readings. Queries always look at recent windows, and old data can be stored cheaply. It wants a purpose-built database rather than a large relational one. Which type fits?

- A. A time-series database
- B. A ledger database
- C. A graph database
- D. A document database

> [!success]- Answer
> **A.** Time-series databases store recent data in memory and older data in cheaper storage. The other types suit different data shapes.
>
> *Task 4.3.* Review: [[15 ElastiCache and Other Databases#Amazon Timestream|Amazon Timestream]]

**59.** A team's EBS volumes must have an RPO of one hour. What is the simplest way to achieve this?

- A. Enable EBS Multi-Attach
- B. Take a monthly AMI
- C. Use Amazon S3 Replication on the volumes
- D. Use Data Lifecycle Manager or AWS Backup to take snapshots every hour

> [!success]- Answer
> **D.** Hourly snapshots meet an RPO of an hour. S3 Replication does not apply to volumes. Monthly images are far too infrequent. Multi-Attach does not back up data.
>
> *Task 2.2.* Review: [[28 High Availability and Disaster Recovery#Backup strategy|Backup strategy]]

**60.** An application uses Route 53 failover. The primary site is in private subnets behind an internal load balancer, so Route 53 health checkers cannot reach it. How can failover still work?

- A. Open the internal load balancer to the internet for health checks only
- B. Use a TXT record to report health
- C. Use a calculated health check with no child checks
- D. Create a CloudWatch alarm for the application's health, and a Route 53 health check based on that alarm

> [!success]- Answer
> **D.** Alarm-based health checks suit private resources. Exposing the load balancer breaks the design. A calculated check needs child checks.
>
> *Task 2.2.* Review: [[11 Route 53#Health checks|Health checks]]

**61.** A multi-Region application needs clients to reach the healthy Region within a minute of a failure. Clients and resolvers cache DNS for a long time, and a static entry point is required. What should a solutions architect use?

- A. Route 53 simple routing with a low TTL
- B. Route 53 latency routing
- C. AWS Global Accelerator
- D. CloudFront with a single origin

> [!success]- Answer
> **C.** Global Accelerator keeps the same IPs and moves traffic inside the network. DNS-based approaches depend on what clients have cached.
>
> *Task 2.2.* Review: [[12 CloudFront and Global Accelerator#AWS Global Accelerator|AWS Global Accelerator]]

**62.** Which two workloads are better suited to containers on AWS Fargate than to AWS Lambda? (Choose two.)

- A. A service that keeps a long-lived process running for hours
- B. A 200 ms function that runs when objects land in S3
- C. A nightly 30-second clean-up task
- D. A job that takes 45 minutes to finish
- E. An API with short requests and long idle periods

> [!success]- Answer
> **A and D.** Long-running processes and jobs over 15 minutes do not fit Lambda. The other three are short and event-driven, which is where Lambda does best.
>
> *Task 2.1.* Review: [[16 Lambda and Serverless#When to use serverless|When to use serverless]]

**63.** A company must encrypt a large number of existing EBS snapshots that were created unencrypted, and share them with another account. What is the correct method?

- A. Enable EBS encryption by default, and existing snapshots will change
- B. Create an AMI from each snapshot, then make it public
- C. Enable encryption on the existing snapshots
- D. Copy each snapshot with encryption enabled, using a customer managed key, then share the copy and the key

> [!success]- Answer
> **D.** A copy can add encryption, and a customer managed key can be shared. Existing snapshots cannot be encrypted in place. Default encryption applies only to new resources. Public AMIs expose data.
>
> *Task 1.3.* Review: [[08 Block and File Storage#Encryption|Encryption]]

**64.** A VPN to a Transit Gateway gives 1.25 Gbps per tunnel, and the company needs about 5 Gbps of aggregate throughput with standard tunnels. Which feature enables this?

- A. Equal-cost multi-path routing across several VPN connections
- B. A larger customer gateway only
- C. A second virtual private gateway on the VPC
- D. VPC peering between tunnels

> [!success]- Answer
> **A.** ECMP on Transit Gateway spreads traffic across tunnels. A virtual private gateway does not support ECMP this way. Peering is unrelated.
>
> *Task 3.4.* Review: [[10 VPC Connectivity and Hybrid Networking#AWS Transit Gateway|AWS Transit Gateway]]

**65.** A company has heavy DNS traffic to its CloudFront distribution, and it wants to cut Route 53 query charges. What should it use?

- A. CNAME records with a long TTL
- B. Alias records pointing to the distribution
- C. A private hosted zone
- D. Multivalue answer records

> [!success]- Answer
> **B.** Alias queries to AWS resources are free. CNAME queries are charged. A private hosted zone does not serve the public.
>
> *Task 4.4.* Review: [[11 Route 53#CNAME versus Alias|CNAME versus Alias]]

## Score your exam

Mark your answers with the key, then count your correct answers for each domain.

> [!example]- Answer key
> 1: A · 2: A · 3: C · 4: D · 5: A · 6: C · 7: A · 8: B · 9: D · 10: D  
> 11: A, E · 12: B · 13: A · 14: A · 15: B · 16: A · 17: D · 18: D · 19: D · 20: B  
> 21: B · 22: A · 23: C · 24: A · 25: B · 26: B · 27: B · 28: C · 29: C · 30: B, E  
> 31: C · 32: B · 33: C · 34: D · 35: D · 36: D · 37: D · 38: C · 39: A · 40: A  
> 41: C · 42: D · 43: A · 44: D · 45: C · 46: D · 47: C · 48: C · 49: A · 50: A  
> 51: A · 52: A · 53: D · 54: C · 55: A, C · 56: B · 57: A · 58: A · 59: D · 60: D  
> 61: C · 62: A, D · 63: D · 64: A · 65: B  

| Domain | Questions | Your score |
| --- | --- | --- |
| Domain 1: Secure | 3, 4, 5, 9, 11, 13, 18, 19, 26, 29, 30, 34, 35, 38, 42, 47, 48, 53, 56, 63 | ___ / 20 |
| Domain 2: Resilient | 2, 7, 8, 20, 21, 24, 27, 28, 37, 51, 52, 54, 57, 59, 60, 61, 62 | ___ / 17 |
| Domain 3: High-Performing | 1, 6, 10, 15, 16, 23, 32, 36, 39, 43, 44, 45, 49, 55, 64 | ___ / 15 |
| Domain 4: Cost-Optimized | 12, 14, 17, 22, 25, 31, 33, 40, 41, 46, 50, 58, 65 | ___ / 13 |
| **Total** | | **___ / 65** |

Add your result to the table in the [[Study Guide#Tracking your progress|Study Guide]], and every mistake to the [[Mistake Log]].

---
**Previous:** [[Practice Exam 2]] · **Next:** [[Practice Exam 4]] · **Plan:** [[Study Guide]]
