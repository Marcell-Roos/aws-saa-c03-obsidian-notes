---
tags: [exam, scope/in]
aliases: ["Domain 4"]
---

# Domain 4: Design Cost-Optimized Architectures

**20% of scored content.** This domain asks for the cheapest option that still meets every requirement. Remove options that break a requirement first, then compare costs. [[29 Cost Optimisation]] is the main chapter.

> [!info] How to use this page
> Each row is an item from AWS's exam guide, word for word. If you can explain the middle column without help, you have covered that item. Follow the link if you cannot.

**Main chapters:** [[29 Cost Optimisation|Cost Optimisation]] · [[04 Amazon EC2|Amazon EC2]] · [[06 Amazon S3|Amazon S3]] · [[10 VPC Connectivity and Hybrid Networking|VPC Connectivity and Hybrid Networking]]

## Task 4.1

**Design cost-optimized storage solutions**

Spend less on storage while meeting requirements. Expect S3 classes, lifecycle rules and gp3.

### Knowledge of

| Exam guide item | What you need to know | Where |
| --- | --- | --- |
| Access options (for example, an S3 bucket with Requester Pays object storage) | Requester Pays moves download costs to the requester. | [[06 Amazon S3#Other features\|Other features]] |
| AWS cost management service features (for example, cost allocation tags, multi-account billing) | Tags and consolidated billing. | [[29 Cost Optimisation#Cost allocation tags\|Cost allocation tags]], [[03 Multi-Account Governance#AWS Organizations\|AWS Organizations]] |
| AWS cost management tools with appropriate use cases (for example, AWS Cost Explorer, AWS Budgets, AWS Cost and Usage Report) | Cost Explorer analyses, Budgets alert, CUR gives detail. | [[29 Cost Optimisation#Cost tools\|Cost tools]] |
| AWS storage services with appropriate use cases (for example, Amazon FSx, Amazon EFS, Amazon S3, Amazon EBS) | Compare services for a workload. | [[29 Cost Optimisation#Storage costs\|Storage costs]], [[08 Block and File Storage#Choosing storage\|Choosing storage]] |
| Backup strategies | Snapshots, AWS Backup and cold storage. | [[28 High Availability and Disaster Recovery#Backup strategy\|Backup strategy]] |
| Block storage options (for example, hard disk drive [HDD] volume types, solid state drive [SSD] volume types) | SSD or HDD, gp3 or io2, st1 or sc1. | [[08 Block and File Storage#Volume types\|Volume types]] |
| Data lifecycles | Move data down the waterfall as it ages. | [[06 Amazon S3#Lifecycle rules\|Lifecycle rules]] |
| Hybrid storage options (for example, AWS DataSync, AWS Transfer Family, AWS Storage Gateway) | DataSync, Transfer Family and Storage Gateway. | [[27 Migration and Data Transfer#Choosing a migration service\|Choosing a migration service]] |
| Storage access patterns | How often data is read decides its class. | [[06 Amazon S3#How to choose\|How to choose]] |
| Storage tiering (for example, cold tiering for object storage) | Glacier classes and Intelligent-Tiering. | [[06 Amazon S3#Storage classes\|Storage classes]] |
| Storage types with associated characteristics (for example, object, file, block) | Object, file and block. | [[08 Block and File Storage#Three kinds of storage\|Three kinds of storage]] |

### Skills in

| Exam guide item | What you need to do | Where |
| --- | --- | --- |
| Designing appropriate storage strategies (for example, batch uploads to Amazon S3 compared with individual uploads) | Group small objects, because S3 charges per request. | [[29 Cost Optimisation#Storage costs\|Storage costs]] |
| Determining the correct storage size for a workload | You pay for provisioned EBS. S3 and EFS bill for use. | [[29 Cost Optimisation#Storage costs\|Storage costs]], [[08 Block and File Storage#Three kinds of storage\|Three kinds of storage]] |
| Determining the lowest cost method of transferring data for a workload to AWS storage | Compare network and physical transfer. | [[27 Migration and Data Transfer#Choosing a transfer method\|Choosing a transfer method]] |
| Determining when storage auto scaling is required | RDS Storage Auto Scaling, and services that grow by themselves. | [[13 RDS and Aurora#Instance and storage\|Instance and storage]], [[29 Cost Optimisation#Storage costs\|Storage costs]] |
| Managing S3 object lifecycles | Transitions, expirations and noncurrent versions. | [[06 Amazon S3#Lifecycle rules\|Lifecycle rules]] |
| Selecting the appropriate backup and/or archival solution | AWS Backup, Glacier classes and Snapshot Archive. | [[28 High Availability and Disaster Recovery#AWS Backup\|AWS Backup]], [[06 Amazon S3#Glacier retrieval options\|Glacier retrieval options]], [[08 Block and File Storage#Snapshots\|Snapshots]] |
| Selecting the appropriate service for data migration to storage services | Match the service to files, databases or servers. | [[27 Migration and Data Transfer#Choosing a migration service\|Choosing a migration service]] |
| Selecting the appropriate storage tier | Use the storage class flow chart. | [[06 Amazon S3#How to choose\|How to choose]] |
| Selecting the correct data lifecycle for storage | Lifecycle rules, and minimum storage durations. | [[06 Amazon S3#Lifecycle rules\|Lifecycle rules]], [[06 Amazon S3#Storage classes\|Storage classes]] |
| Selecting the most cost-effective storage service for a workload | Cheapest option that meets the requirement. | [[08 Block and File Storage#Choosing storage\|Choosing storage]], [[29 Cost Optimisation#Storage costs\|Storage costs]] |

## Task 4.2

**Design cost-optimized compute solutions**

Spend less on compute. Expect Spot, Savings Plans, rightsizing and scaling.

### Knowledge of

| Exam guide item | What you need to know | Where |
| --- | --- | --- |
| AWS cost management service features (for example, cost allocation tags, multi-account billing) | Tags and consolidated billing. | [[29 Cost Optimisation#Cost allocation tags\|Cost allocation tags]], [[03 Multi-Account Governance#AWS Organizations\|AWS Organizations]] |
| AWS cost management tools with appropriate use cases (for example, AWS Cost Explorer, AWS Budgets, AWS Cost and Usage Report) | Cost Explorer, Budgets, CUR and Compute Optimizer. | [[29 Cost Optimisation#Cost tools\|Cost tools]] |
| AWS global infrastructure (for example, Availability Zones, AWS Regions) | Prices differ by Region, and traffic between AZs costs money. | [[01 Cloud Foundations#Choosing a Region\|Choosing a Region]], [[29 Cost Optimisation#Network costs\|Network costs]] |
| AWS purchasing options (for example, Spot Instances, Reserved Instances, Savings Plans) | On-Demand, RIs, Savings Plans, Spot and capacity options. | [[04 Amazon EC2#Purchasing options\|Purchasing options]] |
| Distributed compute strategies (for example, edge processing) | Process near the data or users. | [[19 Other Compute Services#Edge processing\|Edge processing]] |
| Hybrid compute options (for example, AWS Outposts) | Outposts and other hybrid options. | [[19 Other Compute Services#AWS Outposts\|AWS Outposts]] |
| Instance types, families, and sizes (for example, memory optimized, compute optimized, virtualization) | Families, sizes and virtualisation, including Graviton. | [[04 Amazon EC2#Instance types\|Instance types]] |
| Optimization of compute utilization (for example, containers, serverless computing, microservices) | Containers and serverless improve utilisation. | [[29 Cost Optimisation#Compute costs\|Compute costs]] |
| Scaling strategies (for example, auto scaling, hibernation) | Auto Scaling, and hibernation for idle periods. | [[05 Load Balancing and Auto Scaling#Amazon EC2 Auto Scaling\|Amazon EC2 Auto Scaling]], [[04 Amazon EC2#Hibernation\|Hibernation]] |

### Skills in

| Exam guide item | What you need to do | Where |
| --- | --- | --- |
| Determining an appropriate load balancing strategy (for example, Application Load Balancer [Layer 7] compared with Network Load Balancer [Layer 4] compared with Gateway Load Balancer) | Use the simplest load balancer that meets the need. | [[05 Load Balancing and Auto Scaling#Choosing a load balancer\|Choosing a load balancer]], [[29 Cost Optimisation#Load balancer costs\|Load balancer costs]] |
| Determining appropriate scaling methods and strategies for elastic workloads (for example, horizontal compared with vertical, EC2 hibernation) | Horizontal for elastic work, hibernation for idle work. | [[31 Architecture Patterns#Horizontal and vertical scaling\|Horizontal and vertical scaling]], [[04 Amazon EC2#Hibernation\|Hibernation]] |
| Determining cost-effective AWS compute services with appropriate use cases (for example, AWS Lambda, Amazon EC2, AWS Fargate) | Compare Lambda, EC2 and Fargate on usage pattern. | [[19 Other Compute Services#Choosing compute\|Choosing compute]], [[29 Cost Optimisation#Compute costs\|Compute costs]] |
| Determining the required availability for different classes of workloads (for example, production workloads, non-production workloads) | Do not pay for resilience that a workload does not need. | [[29 Cost Optimisation#Availability for each class of workload\|Availability for each class of workload]] |
| Selecting the appropriate instance family for a workload | Match the family to the bottleneck. | [[04 Amazon EC2#Instance types\|Instance types]] |
| Selecting the appropriate instance size for a workload | Rightsize with Compute Optimizer. | [[29 Cost Optimisation#AWS Compute Optimizer\|AWS Compute Optimizer]] |

## Task 4.3

**Design cost-optimized database solutions**

Spend less on databases. Expect serverless options, caching, retention and migrating away from licences.

### Knowledge of

| Exam guide item | What you need to know | Where |
| --- | --- | --- |
| AWS cost management service features (for example, cost allocation tags, multi-account billing) | Tags and consolidated billing. | [[29 Cost Optimisation#Cost allocation tags\|Cost allocation tags]], [[03 Multi-Account Governance#AWS Organizations\|AWS Organizations]] |
| AWS cost management tools with appropriate use cases (for example, AWS Cost Explorer, AWS Budgets, AWS Cost and Usage Report) | Cost Explorer, Budgets and CUR. | [[29 Cost Optimisation#Cost tools\|Cost tools]] |
| Caching strategies | A cache can allow a smaller database. | [[15 ElastiCache and Other Databases#Caching strategies\|Caching strategies]] |
| Data retention policies | Automated backups up to 35 days, snapshots for longer, DynamoDB TTL. | [[13 RDS and Aurora#Backups and restore\|Backups and restore]], [[14 DynamoDB#Backups and S3 integration\|Backups and S3 integration]], [[14 DynamoDB#Time to live\|Time to live]] |
| Database capacity planning (for example, capacity units) | Capacity units, and on-demand or provisioned. | [[14 DynamoDB#Capacity modes\|Capacity modes]] |
| Database connections and proxies | RDS Proxy can avoid a larger instance. | [[13 RDS and Aurora#RDS Proxy\|RDS Proxy]] |
| Database engines with appropriate use cases (for example, heterogeneous migrations, homogeneous migrations) | Moving from commercial to open-source engines. | [[27 Migration and Data Transfer#AWS DMS\|AWS DMS]] |
| Database replication (for example, read replicas) | Read replicas can avoid a bigger primary. Cross-Region replication is charged. | [[13 RDS and Aurora#Read replicas\|Read replicas]] |
| Database types and services (for example, relational compared with non-relational, Amazon Aurora, Amazon DynamoDB) | Relational or non-relational, Aurora or DynamoDB. | [[15 ElastiCache and Other Databases#Choosing a database\|Choosing a database]] |

### Skills in

| Exam guide item | What you need to do | Where |
| --- | --- | --- |
| Designing appropriate backup and retention policies (for example, snapshot frequency) | Set snapshot frequency from the RPO, and retention from the rules. | [[28 High Availability and Disaster Recovery#Backup strategy\|Backup strategy]] |
| Determining an appropriate database engine (for example, MySQL compared with PostgreSQL) | Open-source engines remove licence costs. | [[13 RDS and Aurora#Amazon RDS\|Amazon RDS]] |
| Determining cost-effective AWS database services with appropriate use cases (for example, DynamoDB compared with Amazon RDS, serverless) | Compare by traffic pattern and data model. | [[29 Cost Optimisation#Database costs\|Database costs]] |
| Determining cost-effective AWS database types (for example, time series format, columnar format) | Time series and columnar stores for those data shapes. | [[15 ElastiCache and Other Databases#Amazon Timestream\|Amazon Timestream]], [[22 Data Lakes and Analytics#Amazon Redshift\|Amazon Redshift]] |
| Migrating database schemas and data to different locations and/or different database engines | SCT or DMS Schema Conversion, then DMS. | [[27 Migration and Data Transfer#AWS DMS\|AWS DMS]] |

## Task 4.4

**Design cost-optimized network architectures**

Spend less on data transfer. Expect NAT, endpoints, peering, Transit Gateway and Direct Connect.

### Knowledge of

| Exam guide item | What you need to know | Where |
| --- | --- | --- |
| AWS cost management service features (for example, cost allocation tags, multi-account billing) | Tags and consolidated billing. | [[29 Cost Optimisation#Cost allocation tags\|Cost allocation tags]], [[03 Multi-Account Governance#AWS Organizations\|AWS Organizations]] |
| AWS cost management tools with appropriate use cases (for example, AWS Cost Explorer, AWS Budgets, AWS Cost and Usage Report) | Cost Explorer, Budgets and CUR. | [[29 Cost Optimisation#Cost tools\|Cost tools]] |
| Load balancing concepts (for example, ALB) | Cross-zone charges differ by load balancer. | [[05 Load Balancing and Auto Scaling#Cross-zone load balancing\|Cross-zone load balancing]], [[29 Cost Optimisation#Load balancer costs\|Load balancer costs]] |
| NAT gateways (for example, NAT instance costs compared with NAT gateway costs) | Compare gateway and instance costs, and a shared gateway with one per AZ. | [[09 VPC Fundamentals#NAT for private subnets\|NAT for private subnets]] |
| Network connectivity (for example, private lines, dedicated lines, VPNs) | VPN, Direct Connect, and costs for each. | [[29 Cost Optimisation#Connection choices\|Connection choices]] |
| Network routing, topology, and peering (for example, AWS Transit Gateway, VPC peering) | Peering has no hourly fee. Transit Gateway charges per attachment. | [[29 Cost Optimisation#Connection choices\|Connection choices]], [[10 VPC Connectivity and Hybrid Networking#VPC peering\|VPC peering]] |
| Network services with appropriate use cases (for example, DNS) | Alias queries to AWS resources are free. | [[11 Route 53#CNAME versus Alias\|CNAME versus Alias]] |

### Skills in

| Exam guide item | What you need to do | Where |
| --- | --- | --- |
| Configuring appropriate NAT gateway types for a network (for example, a single shared NAT gateway compared with NAT gateways for each Availability Zone) | One per AZ avoids cross-AZ charges and a single point of failure. | [[09 VPC Fundamentals#NAT for private subnets\|NAT for private subnets]] |
| Configuring appropriate network connections (for example, AWS Direct Connect compared with VPN compared with internet) | Choose by bandwidth, consistency and time to set up. | [[29 Cost Optimisation#Connection choices\|Connection choices]], [[10 VPC Connectivity and Hybrid Networking#Choosing a connection\|Choosing a connection]] |
| Configuring appropriate network routes to minimize network transfer costs (for example, Region to Region, Availability Zone to Availability Zone, private to public, AWS Global Accelerator, VPC endpoints) | Same-AZ traffic, gateway endpoints and private IPs. | [[29 Cost Optimisation#Network costs\|Network costs]] |
| Determining strategic needs for content delivery networks (CDNs) and edge caching | CloudFront lowers origin traffic and data-out cost. | [[12 CloudFront and Global Accelerator#Caching\|Caching]], [[29 Cost Optimisation#Network costs\|Network costs]] |
| Reviewing existing workloads for network optimizations | Find cross-AZ, NAT and internet traffic, using Flow Logs and Cost Explorer. | [[29 Cost Optimisation#Network costs\|Network costs]], [[09 VPC Fundamentals#VPC Flow Logs\|VPC Flow Logs]] |
| Selecting an appropriate throttling strategy | API Gateway limits and WAF rate rules protect back-end spending. | [[17 API Gateway and Front-End Services#Throttling and usage plans\|Throttling and usage plans]] |
| Selecting the appropriate bandwidth allocation for a network device (for example, a single VPN compared with multiple VPNs, Direct Connect speed) | VPN tunnels, ECMP and Direct Connect speeds. | [[29 Cost Optimisation#Connection choices\|Connection choices]] |

---
**Previous:** [[Domain 3 Design High-Performing Architectures]] · **Up:** [[SAA-C03 Exam Overview]]
