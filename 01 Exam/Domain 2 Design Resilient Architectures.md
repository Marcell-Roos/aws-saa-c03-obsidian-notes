---
tags: [exam, scope/in]
aliases: ["Domain 2"]
---

# Domain 2: Design Resilient Architectures

**26% of scored content.** This domain is about systems that scale and survive failure. Task 2.1 is the longest list in the guide, so expect a lot of questions on decoupling, containers and serverless. Prefer loosely coupled, Multi-AZ, managed designs.

> [!info] How to use this page
> Each row is an item from AWS's exam guide, word for word. If you can explain the middle column without help, you have covered that item. Follow the link if you cannot.

**Main chapters:** [[05 Load Balancing and Auto Scaling|Load Balancing and Auto Scaling]] · [[13 RDS and Aurora|RDS and Aurora]] · [[16 Lambda and Serverless|Lambda and Serverless]] · [[18 Containers|Containers]] · [[20 Messaging and Integration|Messaging and Integration]] · [[28 High Availability and Disaster Recovery|High Availability and Disaster Recovery]] · [[31 Architecture Patterns|Architecture Patterns]]

## Task 2.1

**Design scalable and loosely coupled architectures**

Build systems whose parts scale and fail independently. Expect queues, events, containers, serverless and caching.

### Knowledge of

| Exam guide item | What you need to know | Where |
| --- | --- | --- |
| API creation and management (for example, Amazon API Gateway, REST API) | REST, HTTP and WebSocket APIs, endpoint types, throttling and caching. | [[17 API Gateway and Front-End Services#Amazon API Gateway\|Amazon API Gateway]] |
| AWS managed services with appropriate use cases (for example, AWS Transfer Family, Amazon SQS, AWS Secrets Manager) | Know what each managed service replaces. | [[27 Migration and Data Transfer#AWS Transfer Family\|AWS Transfer Family]], [[20 Messaging and Integration#Amazon SQS\|Amazon SQS]], [[23 Encryption and Secrets#AWS Secrets Manager\|AWS Secrets Manager]] |
| Caching strategies | Lazy loading, write-through, TTL, and caching at each layer. | [[15 ElastiCache and Other Databases#Caching strategies\|Caching strategies]] |
| Design principles for microservices (for example, stateless workloads compared with stateful workloads) | Small services with their own data, and stateless tiers. | [[31 Architecture Patterns#Microservices\|Microservices]], [[31 Architecture Patterns#Stateless and stateful workloads\|Stateless and stateful workloads]] |
| Event-driven architectures | Producers and consumers do not know about each other. | [[31 Architecture Patterns#Event-driven architecture\|Event-driven architecture]], [[20 Messaging and Integration#Amazon EventBridge\|Amazon EventBridge]] |
| Horizontal scaling and vertical scaling | Horizontal adds instances. Vertical makes one bigger. | [[31 Architecture Patterns#Horizontal and vertical scaling\|Horizontal and vertical scaling]] |
| How to appropriately use edge accelerators (for example, content delivery network [CDN]) | CloudFront caches content. Global Accelerator speeds routing. | [[12 CloudFront and Global Accelerator#Choosing between them\|Choosing between them]] |
| How to migrate applications into containers | Containerise, store images in ECR, move state out, run on ECS or EKS. | [[18 Containers#Moving an application into containers\|Moving an application into containers]] |
| Load balancing concepts (for example, Application Load Balancer [ALB]) | ALB, NLB and GWLB, target groups and health checks. | [[05 Load Balancing and Auto Scaling#Elastic Load Balancing\|Elastic Load Balancing]] |
| Multi-tier architectures | Separate presentation, application and data tiers. | [[31 Architecture Patterns#Multi-tier architecture\|Multi-tier architecture]] |
| Queuing and messaging concepts (for example, publish/subscribe) | Queues, topics and fan-out. | [[20 Messaging and Integration#Why decouple\|Why decouple]], [[20 Messaging and Integration#Fan-out\|Fan-out]] |
| Serverless technologies and patterns (for example, AWS Fargate, AWS Lambda) | Lambda, Fargate and the building blocks around them. | [[16 Lambda and Serverless#What serverless means\|What serverless means]], [[18 Containers#AWS Fargate\|AWS Fargate]] |
| Storage types with associated characteristics (for example, object, file, block) | Object, file and block storage, and when to use each. | [[08 Block and File Storage#Three kinds of storage\|Three kinds of storage]] |
| The orchestration of containers (for example, Amazon ECS, Amazon EKS) | ECS tasks and services, EKS, and Fargate as a capacity option. | [[18 Containers#Amazon ECS\|Amazon ECS]], [[18 Containers#Amazon EKS\|Amazon EKS]] |
| When to use read replicas | Replicas scale reads. They do not provide automatic failover. | [[13 RDS and Aurora#Read replicas\|Read replicas]] |
| Workflow orchestration (for example, AWS Step Functions) | Step Functions, Standard and Express. | [[20 Messaging and Integration#AWS Step Functions\|AWS Step Functions]] |

### Skills in

| Exam guide item | What you need to do | Where |
| --- | --- | --- |
| Designing event-driven, microservice, and/or multi-tier architectures based on requirements | Choose the architecture style that matches the requirement. | [[31 Architecture Patterns#Multi-tier architecture\|Multi-tier architecture]], [[31 Architecture Patterns#Event-driven architecture\|Event-driven architecture]], [[31 Architecture Patterns#Microservices\|Microservices]] |
| Determining scaling strategies for components used in an architecture design | Pick the scaling method for each component. | [[31 Architecture Patterns#Horizontal and vertical scaling\|Horizontal and vertical scaling]], [[05 Load Balancing and Auto Scaling#Scaling policies\|Scaling policies]] |
| Determining the AWS services required to achieve loose coupling based on requirements | SQS, SNS, EventBridge, Kinesis and load balancers. | [[31 Architecture Patterns#Loose coupling\|Loose coupling]] |
| Determining when to use containers | Long-running or portable workloads, and existing container images. | [[18 Containers#Containers in brief\|Containers in brief]] |
| Determining when to use serverless technologies and patterns | Short, event-driven and spiky workloads. | [[16 Lambda and Serverless#When to use serverless\|When to use serverless]] |
| Recommending appropriate compute, storage, networking, and database technologies based on requirements | Use the selection guides for each area. | [[19 Other Compute Services#Choosing compute\|Choosing compute]], [[08 Block and File Storage#Choosing storage\|Choosing storage]], [[15 ElastiCache and Other Databases#Choosing a database\|Choosing a database]], [[10 VPC Connectivity and Hybrid Networking#Choosing a connection\|Choosing a connection]] |
| Using purpose-built AWS services for workloads | Choose the database or service built for the access pattern. | [[15 ElastiCache and Other Databases#Choosing a database\|Choosing a database]] |

## Task 2.2

**Design highly available and/or fault-tolerant architectures**

Survive failure. Expect Multi-AZ, DR strategies, Route 53 failover, backups and RDS Proxy.

### Knowledge of

| Exam guide item | What you need to know | Where |
| --- | --- | --- |
| AWS global infrastructure (for example, Availability Zones, AWS Regions, Amazon Route 53) | AZs for local failures, Regions for large ones, Route 53 between them. | [[01 Cloud Foundations#The global infrastructure\|The global infrastructure]], [[11 Route 53#Routing policies\|Routing policies]] |
| AWS managed services with appropriate use cases (for example, Amazon Comprehend, Amazon Polly) | Know each managed AI service by its input and output. | [[30 Machine Learning Services#In-scope services\|In-scope services]] |
| Basic networking concepts (for example, route tables) | Route tables, gateways and the local route. | [[09 VPC Fundamentals#Internet gateways and route tables\|Internet gateways and route tables]] |
| Disaster recovery (DR) strategies (for example, backup and restore, pilot light, warm standby, active-active failover, recovery point objective [RPO], recovery time objective [RTO]) | Four strategies, and how RPO and RTO choose between them. | [[28 High Availability and Disaster Recovery#Disaster recovery strategies\|Disaster recovery strategies]], [[28 High Availability and Disaster Recovery#RPO and RTO\|RPO and RTO]] |
| Distributed design patterns | Retries with backoff, idempotency, load levelling and timeouts. | [[28 High Availability and Disaster Recovery#Distributed design patterns\|Distributed design patterns]] |
| Failover strategies | Multi-AZ, Route 53 failover and Global Accelerator. | [[28 High Availability and Disaster Recovery#Building blocks for each layer\|Building blocks for each layer]], [[11 Route 53#Failover\|Failover]] |
| Immutable infrastructure | Replace servers rather than changing them. | [[26 Infrastructure as Code and Operations#Immutable infrastructure\|Immutable infrastructure]] |
| Load balancing concepts (for example, ALB) | Health checks remove failed targets. | [[05 Load Balancing and Auto Scaling#Listeners and target groups\|Listeners and target groups]] |
| Proxy concepts (for example, Amazon RDS Proxy) | RDS Proxy pools connections and shortens failover. | [[13 RDS and Aurora#RDS Proxy\|RDS Proxy]] |
| Service quotas and throttling (for example, how to configure the service quotas for a workload in a standby environment) | Quotas are per Region. Raise them in standby Regions in advance. Handle throttling with backoff. | [[28 High Availability and Disaster Recovery#Quotas in a standby Region\|Quotas in a standby Region]], [[01 Cloud Foundations#Service quotas and throttling\|Service quotas and throttling]] |
| Storage options and characteristics (for example, durability, replication) | Durability and availability of each storage class and service. | [[06 Amazon S3#Storage classes\|Storage classes]], [[08 Block and File Storage#Three kinds of storage\|Three kinds of storage]] |
| Workload visibility (for example, AWS X-Ray) | X-Ray traces requests. CloudWatch shows metrics and logs. | [[25 Monitoring and Auditing#AWS X-Ray\|AWS X-Ray]], [[25 Monitoring and Auditing#Amazon CloudWatch\|Amazon CloudWatch]] |

### Skills in

| Exam guide item | What you need to do | Where |
| --- | --- | --- |
| Determining automation strategies to ensure infrastructure integrity | CloudFormation, Config remediation and immutable deployments. | [[26 Infrastructure as Code and Operations#AWS CloudFormation\|AWS CloudFormation]], [[25 Monitoring and Auditing#AWS Config\|AWS Config]] |
| Determining the AWS services required to provide a highly available and/or fault-tolerant architecture across AWS Regions or Availability Zones | Choose the right service at each layer for AZ or Region failure. | [[28 High Availability and Disaster Recovery#Building blocks for each layer\|Building blocks for each layer]] |
| Identifying metrics based on business requirements to deliver a highly available solution | Choose signals that reflect the user's experience. | [[25 Monitoring and Auditing#Choosing metrics\|Choosing metrics]] |
| Implementing designs to mitigate single points of failure | Check each layer for one thing whose loss stops the workload. | [[28 High Availability and Disaster Recovery#Removing single points of failure\|Removing single points of failure]] |
| Implementing strategies to ensure the durability and availability of data (for example, backups) | Backups, replication and vault locks. | [[28 High Availability and Disaster Recovery#Backup strategy\|Backup strategy]], [[28 High Availability and Disaster Recovery#AWS Backup\|AWS Backup]] |
| Selecting an appropriate DR strategy to meet business requirements | The cheapest strategy that meets the RPO and RTO. | [[28 High Availability and Disaster Recovery#Disaster recovery strategies\|Disaster recovery strategies]] |
| Using AWS services that improve the reliability of legacy applications and applications not built for the cloud (for example, when application changes are not possible) | Add resilience around an application that cannot be changed. | [[28 High Availability and Disaster Recovery#Making legacy applications more reliable\|Making legacy applications more reliable]] |
| Using purpose-built AWS services for workloads | Choose the managed service built for the job. | [[15 ElastiCache and Other Databases#Choosing a database\|Choosing a database]], [[30 Machine Learning Services#In-scope services\|In-scope services]] |

---
**Previous:** [[Domain 1 Design Secure Architectures]] · **Next:** [[Domain 3 Design High-Performing Architectures]] · **Up:** [[SAA-C03 Exam Overview]]
