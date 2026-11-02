---
tags: [exam, scope/in]
aliases: ["Domain 3"]
---

# Domain 3: Design High-Performing Architectures

**24% of scored content.** This domain asks you to pick the right service and configuration for a workload. The answer usually depends on an access pattern, a size or a speed. Look for numbers in the question.

> [!info] How to use this page
> Each row is an item from AWS's exam guide, word for word. If you can explain the middle column without help, you have covered that item. Follow the link if you cannot.

**Main chapters:** [[04 Amazon EC2|Amazon EC2]] · [[06 Amazon S3|Amazon S3]] · [[08 Block and File Storage|Block and File Storage]] · [[12 CloudFront and Global Accelerator|CloudFront and Global Accelerator]] · [[14 DynamoDB|DynamoDB]] · [[15 ElastiCache and Other Databases|ElastiCache and Other Databases]] · [[21 Streaming and Data Ingestion|Streaming and Data Ingestion]] · [[22 Data Lakes and Analytics|Data Lakes and Analytics]]

## Task 3.1

**Determine high-performing and/or scalable storage solutions**

Choose storage that meets performance needs and can grow.

### Knowledge of

| Exam guide item | What you need to know | Where |
| --- | --- | --- |
| Hybrid storage solutions to meet business requirements | Storage Gateway, DataSync and FSx for hybrid access. | [[27 Migration and Data Transfer#AWS Storage Gateway\|AWS Storage Gateway]] |
| Storage services with appropriate use cases (for example, Amazon S3, Amazon EFS, Amazon EBS) | When to use S3, EFS, EBS and FSx. | [[08 Block and File Storage#Choosing storage\|Choosing storage]], [[06 Amazon S3#The basics\|The basics]] |
| Storage types with associated characteristics (for example, object, file, block) | Object, file and block, and how they behave. | [[08 Block and File Storage#Three kinds of storage\|Three kinds of storage]] |

### Skills in

| Exam guide item | What you need to do | Where |
| --- | --- | --- |
| Determining storage services and configurations that meet performance demands | EBS types and IOPS, S3 request rates, EFS modes, FSx options. | [[08 Block and File Storage#Volume types\|Volume types]], [[06 Amazon S3#Performance\|Performance]], [[08 Block and File Storage#Amazon FSx\|Amazon FSx]] |
| Determining storage services that can scale to accommodate future needs | S3 and EFS grow automatically. EBS must be resized. | [[08 Block and File Storage#Amazon EFS\|Amazon EFS]], [[06 Amazon S3#The basics\|The basics]] |

## Task 3.2

**Design high-performing and elastic compute solutions**

Choose compute that performs well and scales. Expect instance families, Auto Scaling metrics and Lambda memory.

### Knowledge of

| Exam guide item | What you need to know | Where |
| --- | --- | --- |
| AWS compute services with appropriate use cases (for example, AWS Batch, Amazon EMR, AWS Fargate) | Batch for batch jobs, EMR for big data, Fargate for serverless containers. | [[19 Other Compute Services#AWS Batch\|AWS Batch]], [[22 Data Lakes and Analytics#Amazon EMR\|Amazon EMR]], [[18 Containers#AWS Fargate\|AWS Fargate]] |
| Distributed computing concepts supported by AWS global infrastructure and edge services | Spread work across AZs, Regions and the edge. | [[19 Other Compute Services#Running AWS closer to users\|Running AWS closer to users]], [[19 Other Compute Services#Edge processing\|Edge processing]] |
| Queuing and messaging concepts (for example, publish/subscribe) | Queues and topics let components scale separately. | [[20 Messaging and Integration#Why decouple\|Why decouple]] |
| Scalability capabilities with appropriate use cases (for example, Amazon EC2 Auto Scaling, AWS Auto Scaling) | EC2 Auto Scaling, Application Auto Scaling and AWS Auto Scaling. | [[05 Load Balancing and Auto Scaling#Amazon EC2 Auto Scaling\|Amazon EC2 Auto Scaling]], [[05 Load Balancing and Auto Scaling#AWS Auto Scaling and Application Auto Scaling\|AWS Auto Scaling and Application Auto Scaling]] |
| Serverless technologies and patterns (for example, AWS Lambda, Fargate) | Lambda limits and concurrency, and Fargate. | [[16 Lambda and Serverless#AWS Lambda\|AWS Lambda]] |
| The orchestration of containers (for example, Amazon ECS, Amazon EKS) | ECS and EKS. | [[18 Containers#Amazon ECS\|Amazon ECS]], [[18 Containers#Amazon EKS\|Amazon EKS]] |

### Skills in

| Exam guide item | What you need to do | Where |
| --- | --- | --- |
| Decoupling workloads so that components can scale independently | Put a queue between components, and scale each one on its own metric. | [[31 Architecture Patterns#Loose coupling\|Loose coupling]], [[20 Messaging and Integration#Scaling workers on queue depth\|Scaling workers on queue depth]] |
| Identifying metrics and conditions to perform scaling actions | Target tracking, step, scheduled and predictive. Choose the right metric. | [[05 Load Balancing and Auto Scaling#Scaling policies\|Scaling policies]] |
| Selecting the appropriate compute options and features (for example, EC2 instance types) to meet business requirements | Instance families and what each is for. | [[04 Amazon EC2#Instance types\|Instance types]] |
| Selecting the appropriate resource type and size (for example, the amount of Lambda memory) to meet business requirements | Lambda CPU scales with memory. Instance size follows the workload. | [[16 Lambda and Serverless#Limits\|Limits]], [[04 Amazon EC2#Instance types\|Instance types]] |

## Task 3.3

**Determine high-performing database solutions**

Choose and tune databases. Expect replicas, caching, capacity units and engines.

### Knowledge of

| Exam guide item | What you need to know | Where |
| --- | --- | --- |
| AWS global infrastructure (for example, Availability Zones, AWS Regions) | Multi-AZ inside a Region, Global Database and global tables across Regions. | [[13 RDS and Aurora#Aurora Global Database\|Aurora Global Database]], [[14 DynamoDB#Global tables\|Global tables]] |
| Caching strategies and services (for example, Amazon ElastiCache) | Lazy loading, write-through, ElastiCache and DAX. | [[15 ElastiCache and Other Databases#Caching strategies\|Caching strategies]], [[14 DynamoDB#DynamoDB Accelerator\|DynamoDB Accelerator]] |
| Data access patterns (for example, read-intensive compared with write-intensive) | Replicas for reads, bigger or sharded for writes. | [[13 RDS and Aurora#Multi-AZ versus read replicas\|Multi-AZ versus read replicas]] |
| Database capacity planning (for example, capacity units, instance types, Provisioned IOPS) | RCU and WCU, RDS instance types, Provisioned IOPS. | [[14 DynamoDB#Calculating capacity\|Calculating capacity]], [[13 RDS and Aurora#Instance and storage\|Instance and storage]] |
| Database connections and proxies | Connection pools and RDS Proxy. | [[13 RDS and Aurora#RDS Proxy\|RDS Proxy]] |
| Database engines with appropriate use cases (for example, heterogeneous migrations, homogeneous migrations) | Same-engine and different-engine migrations. | [[27 Migration and Data Transfer#AWS DMS\|AWS DMS]] |
| Database replication (for example, read replicas) | Read replicas, Multi-AZ and global replication. | [[13 RDS and Aurora#Read replicas\|Read replicas]] |
| Database types and services (for example, serverless, relational compared with non-relational, in-memory) | Serverless, relational, non-relational and in-memory. | [[15 ElastiCache and Other Databases#Choosing a database\|Choosing a database]] |

### Skills in

| Exam guide item | What you need to do | Where |
| --- | --- | --- |
| Configuring read replicas to meet business requirements | Number, location, promotion, and pointing readers at them. | [[13 RDS and Aurora#Read replicas\|Read replicas]] |
| Designing database architectures | Combine HA, read scaling and caching. | [[13 RDS and Aurora#Multi-AZ versus read replicas\|Multi-AZ versus read replicas]], [[31 Architecture Patterns#Multi-tier architecture\|Multi-tier architecture]] |
| Determining an appropriate database engine (for example, MySQL compared with PostgreSQL) | Follow the application and licences. MySQL and PostgreSQL are both open source. | [[13 RDS and Aurora#Amazon RDS\|Amazon RDS]], [[13 RDS and Aurora#Choosing RDS or Aurora\|Choosing RDS or Aurora]] |
| Determining an appropriate database type (for example, Amazon Aurora, Amazon DynamoDB) | Relational needs SQL. DynamoDB needs key-based access at scale. | [[13 RDS and Aurora#Choosing RDS or Aurora\|Choosing RDS or Aurora]], [[14 DynamoDB#What it is\|What it is]] |
| Integrating caching to meet business requirements | Cache repeated reads, and choose a strategy. | [[15 ElastiCache and Other Databases#Caching strategies\|Caching strategies]] |

## Task 3.4

**Determine high-performing and/or scalable network architectures**

Design networks that perform and scale. Expect CloudFront, load balancers, VPN and Direct Connect.

### Knowledge of

| Exam guide item | What you need to know | Where |
| --- | --- | --- |
| Edge networking services with appropriate use cases (for example, Amazon CloudFront, AWS Global Accelerator) | CloudFront or Global Accelerator. | [[12 CloudFront and Global Accelerator#Choosing between them\|Choosing between them]] |
| How to design network architecture (for example, subnet tiers, routing, IP addressing) | CIDR planning, subnets, tiers and routes. | [[09 VPC Fundamentals#IP addressing and CIDR\|IP addressing and CIDR]], [[09 VPC Fundamentals#Internet gateways and route tables\|Internet gateways and route tables]] |
| Load balancing concepts (for example, Application Load Balancer [ALB]) | ALB, NLB and GWLB. | [[05 Load Balancing and Auto Scaling#Choosing a load balancer\|Choosing a load balancer]] |
| Network connection options (for example, AWS VPN, AWS Direct Connect, AWS PrivateLink) | VPN, Direct Connect, PrivateLink, peering and Transit Gateway. | [[10 VPC Connectivity and Hybrid Networking#Choosing a connection\|Choosing a connection]] |

### Skills in

| Exam guide item | What you need to do | Where |
| --- | --- | --- |
| Creating a network topology for various architectures (for example, global, hybrid, multi-tier) | Multi-tier VPCs, hub-and-spoke, and global designs. | [[10 VPC Connectivity and Hybrid Networking#AWS Transit Gateway\|AWS Transit Gateway]], [[09 VPC Fundamentals#The big picture\|The big picture]] |
| Determining network configurations that can scale to accommodate future needs | Size CIDRs generously, avoid overlaps, and use Transit Gateway to grow. | [[09 VPC Fundamentals#IP addressing and CIDR\|IP addressing and CIDR]], [[10 VPC Connectivity and Hybrid Networking#AWS Transit Gateway\|AWS Transit Gateway]] |
| Determining the appropriate placement of resources to meet business requirements | Region choice, AZ spread, placement groups, and edge locations. | [[01 Cloud Foundations#Choosing a Region\|Choosing a Region]], [[04 Amazon EC2#Placement groups\|Placement groups]], [[19 Other Compute Services#Running AWS closer to users\|Running AWS closer to users]] |
| Selecting the appropriate load balancing strategy | Match layer, protocol and static IP needs to a load balancer. | [[05 Load Balancing and Auto Scaling#Choosing a load balancer\|Choosing a load balancer]] |

## Task 3.5

**Determine high-performing data ingestion and transformation solutions**

Get data in and make it useful. Expect Kinesis, Firehose, Glue, Athena and Lake Formation.

### Knowledge of

| Exam guide item | What you need to know | Where |
| --- | --- | --- |
| Data analytics and visualization services with appropriate use cases (for example, Amazon Athena, AWS Lake Formation, Amazon Quick) | Athena for SQL on S3, Lake Formation for governance, Quick for dashboards. | [[22 Data Lakes and Analytics#Amazon Athena\|Amazon Athena]], [[22 Data Lakes and Analytics#AWS Lake Formation\|AWS Lake Formation]], [[22 Data Lakes and Analytics#Amazon Quick\|Amazon Quick]] |
| Data ingestion patterns (for example, frequency) | Real time, near real time, batch. | [[21 Streaming and Data Ingestion#Choosing an ingestion pattern\|Choosing an ingestion pattern]] |
| Data transfer services with appropriate use cases (for example, AWS DataSync, AWS Storage Gateway) | DataSync moves data. Storage Gateway provides ongoing access. | [[27 Migration and Data Transfer#AWS DataSync\|AWS DataSync]], [[27 Migration and Data Transfer#AWS Storage Gateway\|AWS Storage Gateway]] |
| Data transformation services with appropriate use cases (for example, AWS Glue) | Glue jobs and crawlers. | [[22 Data Lakes and Analytics#AWS Glue\|AWS Glue]] |
| Secure access to ingestion access points | IAM roles, VPC endpoints, encryption and bucket policies. | [[21 Streaming and Data Ingestion#Securing ingestion\|Securing ingestion]] |
| Sizes and speeds needed to meet business requirements | Work out throughput and freshness, then choose. | [[21 Streaming and Data Ingestion#Sizes and speeds\|Sizes and speeds]] |
| Streaming data services with appropriate use cases (for example, Amazon Kinesis) | Kinesis Data Streams, Data Firehose and MSK. | [[21 Streaming and Data Ingestion#Kinesis Data Streams\|Kinesis Data Streams]], [[21 Streaming and Data Ingestion#Amazon Data Firehose\|Amazon Data Firehose]], [[21 Streaming and Data Ingestion#Amazon MSK\|Amazon MSK]] |

### Skills in

| Exam guide item | What you need to do | Where |
| --- | --- | --- |
| Building and securing data lakes | S3 plus Glue plus Lake Formation, with access control and encryption. | [[22 Data Lakes and Analytics#Data lakes\|Data lakes]], [[22 Data Lakes and Analytics#Securing a data lake\|Securing a data lake]] |
| Designing data streaming architectures | Producers, shards, consumers and delivery. | [[21 Streaming and Data Ingestion#Kinesis Data Streams\|Kinesis Data Streams]], [[21 Streaming and Data Ingestion#Amazon Data Firehose\|Amazon Data Firehose]] |
| Designing data transfer solutions | Choose by volume, time and connection. | [[27 Migration and Data Transfer#Choosing a transfer method\|Choosing a transfer method]] |
| Implementing visualization strategies | Amazon Quick for business users, OpenSearch Dashboards and Grafana for operations. | [[22 Data Lakes and Analytics#Amazon Quick\|Amazon Quick]] |
| Selecting appropriate compute options for data processing (for example, Amazon EMR) | EMR for Spark and Hadoop, Glue for serverless ETL, Athena for SQL. | [[22 Data Lakes and Analytics#Amazon EMR\|Amazon EMR]], [[22 Data Lakes and Analytics#Choosing an analytics service\|Choosing an analytics service]] |
| Selecting appropriate configurations for ingestion | Shards, on-demand or provisioned, Firehose buffering. | [[21 Streaming and Data Ingestion#Capacity modes\|Capacity modes]], [[21 Streaming and Data Ingestion#Amazon Data Firehose\|Amazon Data Firehose]] |
| Transforming data between formats (for example, .csv to .parquet) | Glue jobs and Firehose convert to Parquet. | [[22 Data Lakes and Analytics#Data formats\|Data formats]] |

---
**Previous:** [[Domain 2 Design Resilient Architectures]] · **Next:** [[Domain 4 Design Cost-Optimized Architectures]] · **Up:** [[SAA-C03 Exam Overview]]
