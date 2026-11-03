---
tags: [reference, scope/in]
aliases: ["In-Scope Services", "Out-of-Scope Services"]
---

# Service Index

Every service on AWS's in-scope list, what it does, and where it is covered. This list comes from exam guide v1.1, published on 29 October 2026. AWS says that it is non-exhaustive and subject to change. Services in this table are in the same categories as AWS's list.

Use this page as a last check: cover the middle column, and say what each service does.

## In-scope services

### Analytics

| Service | What it does | Chapter |
| --- | --- | --- |
| Amazon Athena | Serverless SQL queries on S3 | [[22 Data Lakes and Analytics#Amazon Athena\|Data Lakes and Analytics]] |
| AWS Data Exchange | Find and subscribe to third-party datasets | [[22 Data Lakes and Analytics#Other services\|Data Lakes and Analytics]] |
| AWS Data Pipeline | Scheduled data movement. Closed to new customers | [[22 Data Lakes and Analytics#Other services\|Data Lakes and Analytics]] |
| Amazon EMR | Managed Hadoop and Spark clusters | [[22 Data Lakes and Analytics#Amazon EMR\|Data Lakes and Analytics]] |
| AWS Glue | Serverless ETL and data catalogue | [[22 Data Lakes and Analytics#AWS Glue\|Data Lakes and Analytics]] |
| Amazon Kinesis | Real-time streaming data | [[21 Streaming and Data Ingestion#Kinesis Data Streams\|Streaming and Data Ingestion]] |
| AWS Lake Formation | Build and secure data lakes | [[22 Data Lakes and Analytics#AWS Lake Formation\|Data Lakes and Analytics]] |
| Amazon Managed Streaming for Apache Kafka (Amazon MSK) | Managed Apache Kafka | [[21 Streaming and Data Ingestion#Amazon MSK\|Streaming and Data Ingestion]] |
| Amazon OpenSearch Service | Search and log analytics | [[22 Data Lakes and Analytics#Amazon OpenSearch Service\|Data Lakes and Analytics]] |
| Amazon Quick | Business intelligence dashboards, formerly QuickSight | [[22 Data Lakes and Analytics#Amazon Quick\|Data Lakes and Analytics]] |
| Amazon Redshift | Petabyte-scale data warehouse | [[22 Data Lakes and Analytics#Amazon Redshift\|Data Lakes and Analytics]] |

### Application Integration

| Service | What it does | Chapter |
| --- | --- | --- |
| Amazon AppFlow | No-code data flows between SaaS apps and AWS | [[20 Messaging and Integration#Other integration services\|Messaging and Integration]] |
| Amazon EventBridge | Serverless event bus and scheduler | [[20 Messaging and Integration#Amazon EventBridge\|Messaging and Integration]] |
| Amazon MQ | Managed RabbitMQ and ActiveMQ | [[20 Messaging and Integration#Amazon MQ\|Messaging and Integration]] |
| Amazon SNS | Publish and subscribe notifications | [[20 Messaging and Integration#Amazon SNS\|Messaging and Integration]] |
| Amazon SQS | Managed message queues | [[20 Messaging and Integration#Amazon SQS\|Messaging and Integration]] |
| AWS Step Functions | Serverless workflow orchestration | [[20 Messaging and Integration#AWS Step Functions\|Messaging and Integration]] |

### AWS Cost Management

| Service | What it does | Chapter |
| --- | --- | --- |
| AWS Budgets | Alerts on cost and usage | [[29 Cost Optimisation#AWS Budgets\|Cost Optimisation]] |
| AWS Cost and Usage Report | Most detailed billing data | [[29 Cost Optimisation#Cost and Usage Report\|Cost Optimisation]] |
| AWS Cost Explorer | Analyse and forecast spending | [[29 Cost Optimisation#AWS Cost Explorer\|Cost Optimisation]] |
| Savings Plans | Discounts for an hourly spending commitment | [[04 Amazon EC2#Savings Plans\|Amazon EC2]] |

### Compute

| Service | What it does | Chapter |
| --- | --- | --- |
| AWS Batch | Managed batch jobs at any scale | [[19 Other Compute Services#AWS Batch\|Other Compute Services]] |
| Amazon EC2 | Virtual machines | [[04 Amazon EC2#What EC2 is\|Amazon EC2]] |
| Amazon EC2 Auto Scaling | Adjusts the number of instances | [[05 Load Balancing and Auto Scaling#Amazon EC2 Auto Scaling\|Load Balancing and Auto Scaling]] |
| AWS Elastic Beanstalk | Deploy applications with the infrastructure handled | [[19 Other Compute Services#AWS Elastic Beanstalk\|Other Compute Services]] |
| AWS Outposts | AWS racks in your own data centre | [[19 Other Compute Services#AWS Outposts\|Other Compute Services]] |
| AWS Serverless Application Repository | Catalogue of serverless applications | [[16 Lambda and Serverless#AWS Serverless Application Repository\|Lambda and Serverless]] |
| VMware Cloud on AWS | Run VMware environments on AWS | [[19 Other Compute Services#VMware Cloud on AWS\|Other Compute Services]] |
| AWS Wavelength | AWS compute inside 5G networks | [[19 Other Compute Services#AWS Wavelength\|Other Compute Services]] |

### Containers

| Service | What it does | Chapter |
| --- | --- | --- |
| Amazon ECR | Container image registry | [[18 Containers#Amazon ECR\|Containers]] |
| Amazon ECS | AWS's container orchestrator | [[18 Containers#Amazon ECS\|Containers]] |
| Amazon ECS Anywhere | ECS tasks on your own servers | [[18 Containers#Where tasks run\|Containers]] |
| Amazon EKS | Managed Kubernetes | [[18 Containers#Amazon EKS\|Containers]] |
| Amazon EKS Anywhere | Kubernetes on your own infrastructure | [[18 Containers#Running Kubernetes elsewhere\|Containers]] |
| Amazon EKS Distro | The Kubernetes distribution used by EKS | [[18 Containers#Running Kubernetes elsewhere\|Containers]] |

### Database

| Service | What it does | Chapter |
| --- | --- | --- |
| Amazon Aurora | Cloud-native relational database | [[13 RDS and Aurora#Amazon Aurora\|RDS and Aurora]] |
| Amazon Aurora Serverless | Aurora that scales automatically | [[13 RDS and Aurora#Aurora Serverless v2\|RDS and Aurora]] |
| Amazon DocumentDB | MongoDB-compatible document database | [[15 ElastiCache and Other Databases#Amazon DocumentDB\|ElastiCache and Other Databases]] |
| Amazon DynamoDB | Serverless NoSQL database | [[14 DynamoDB#What it is\|DynamoDB]] |
| Amazon ElastiCache | In-memory cache | [[15 ElastiCache and Other Databases#Amazon ElastiCache\|ElastiCache and Other Databases]] |
| Amazon Keyspaces | Cassandra-compatible database | [[15 ElastiCache and Other Databases#Amazon Keyspaces\|ElastiCache and Other Databases]] |
| Amazon Neptune | Graph database | [[15 ElastiCache and Other Databases#Amazon Neptune\|ElastiCache and Other Databases]] |
| Amazon RDS | Managed relational databases | [[13 RDS and Aurora#Amazon RDS\|RDS and Aurora]] |
| Amazon Redshift | Data warehouse | [[22 Data Lakes and Analytics#Amazon Redshift\|Data Lakes and Analytics]] |

### Developer Tools

| Service | What it does | Chapter |
| --- | --- | --- |
| AWS X-Ray | Distributed request tracing | [[25 Monitoring and Auditing#AWS X-Ray\|Monitoring and Auditing]] |

### Front-End Web and Mobile

| Service | What it does | Chapter |
| --- | --- | --- |
| AWS Amplify | Build and host full-stack web and mobile apps | [[17 API Gateway and Front-End Services#AWS Amplify\|API Gateway and Front-End Services]] |
| Amazon API Gateway | Create and manage APIs | [[17 API Gateway and Front-End Services#Amazon API Gateway\|API Gateway and Front-End Services]] |
| AWS Device Farm | Test apps on real devices | [[17 API Gateway and Front-End Services#AWS Device Farm\|API Gateway and Front-End Services]] |

### Machine Learning

| Service | What it does | Chapter |
| --- | --- | --- |
| Amazon Comprehend | Natural language processing | [[30 Machine Learning Services#In-scope services\|Machine Learning Services]] |
| Amazon Lex | Chatbots | [[30 Machine Learning Services#In-scope services\|Machine Learning Services]] |
| Amazon Polly | Text to speech | [[30 Machine Learning Services#In-scope services\|Machine Learning Services]] |
| Amazon Rekognition | Image and video analysis | [[30 Machine Learning Services#In-scope services\|Machine Learning Services]] |
| Amazon SageMaker AI | Build and train custom models | [[30 Machine Learning Services#In-scope services\|Machine Learning Services]] |
| Amazon Textract | Extract text and data from documents | [[30 Machine Learning Services#In-scope services\|Machine Learning Services]] |
| Amazon Transcribe | Speech to text | [[30 Machine Learning Services#In-scope services\|Machine Learning Services]] |
| Amazon Translate | Language translation | [[30 Machine Learning Services#In-scope services\|Machine Learning Services]] |

### Management and Governance

| Service | What it does | Chapter |
| --- | --- | --- |
| AWS Auto Scaling | Scaling plans across several services | [[05 Load Balancing and Auto Scaling#AWS Auto Scaling and Application Auto Scaling\|Load Balancing and Auto Scaling]] |
| AWS CLI | Command-line access to AWS | [[01 Cloud Foundations#How you talk to AWS\|Cloud Foundations]] |
| AWS CloudFormation | Infrastructure as code | [[26 Infrastructure as Code and Operations#AWS CloudFormation\|Infrastructure as Code and Operations]] |
| AWS CloudTrail | Records API calls | [[25 Monitoring and Auditing#AWS CloudTrail\|Monitoring and Auditing]] |
| Amazon CloudWatch | Metrics, logs and alarms | [[25 Monitoring and Auditing#Amazon CloudWatch\|Monitoring and Auditing]] |
| AWS Compute Optimizer | Rightsizing recommendations | [[29 Cost Optimisation#AWS Compute Optimizer\|Cost Optimisation]] |
| AWS Config | Records configuration and checks compliance | [[25 Monitoring and Auditing#AWS Config\|Monitoring and Auditing]] |
| AWS Control Tower | Sets up a governed multi-account environment | [[03 Multi-Account Governance#AWS Control Tower\|Multi-Account Governance]] |
| AWS Health Dashboard | Status of AWS and your resources | [[25 Monitoring and Auditing#AWS Health Dashboard\|Monitoring and Auditing]] |
| AWS License Manager | Tracks software licences | [[03 Multi-Account Governance#AWS License Manager\|Multi-Account Governance]] |
| Amazon Managed Grafana | Managed dashboards | [[25 Monitoring and Auditing#Grafana and Prometheus\|Monitoring and Auditing]] |
| Amazon Managed Service for Prometheus | Managed metrics for containers | [[25 Monitoring and Auditing#Grafana and Prometheus\|Monitoring and Auditing]] |
| AWS Management Console | The web interface to AWS | [[01 Cloud Foundations#How you talk to AWS\|Cloud Foundations]] |
| AWS Organizations | Manage many accounts together | [[03 Multi-Account Governance#AWS Organizations\|Multi-Account Governance]] |
| AWS Proton | Templates for platform teams. Support ended | [[26 Infrastructure as Code and Operations#AWS Proton\|Infrastructure as Code and Operations]] |
| AWS Service Catalog | Approved products for self-service | [[03 Multi-Account Governance#AWS Service Catalog\|Multi-Account Governance]] |
| AWS Systems Manager | Manage fleets of servers | [[26 Infrastructure as Code and Operations#AWS Systems Manager\|Infrastructure as Code and Operations]] |
| AWS Well-Architected Tool | Guided workload reviews | [[01 Cloud Foundations#The AWS Well-Architected Framework\|Cloud Foundations]] |

### Media Services

| Service | What it does | Chapter |
| --- | --- | --- |
| Amazon Kinesis Video Streams | Ingest and process video | [[21 Streaming and Data Ingestion#Amazon Kinesis Video Streams\|Streaming and Data Ingestion]] |

### Migration and Transfer

| Service | What it does | Chapter |
| --- | --- | --- |
| AWS Application Discovery Service | Discover on-premises servers. Closed to new customers | [[27 Migration and Data Transfer#Discovery and planning\|Migration and Data Transfer]] |
| AWS Application Migration Service | Lift and shift servers, now branded AWS Transform MGN | [[27 Migration and Data Transfer#AWS Application Migration Service\|Migration and Data Transfer]] |
| AWS DataSync | Move and sync file and object data | [[27 Migration and Data Transfer#AWS DataSync\|Migration and Data Transfer]] |
| AWS DMS | Migrate databases | [[27 Migration and Data Transfer#AWS DMS\|Migration and Data Transfer]] |
| AWS Snow Family | Physical data transfer devices. Closed to new customers, and support for Snowball devices ends 31 December 2026 | [[27 Migration and Data Transfer#AWS Snow Family\|Migration and Data Transfer]] |
| AWS Transfer Family | Managed SFTP, FTPS, FTP and AS2 | [[27 Migration and Data Transfer#AWS Transfer Family\|Migration and Data Transfer]] |

### Networking and Content Delivery

| Service | What it does | Chapter |
| --- | --- | --- |
| AWS Client VPN | VPN for individual users | [[10 VPC Connectivity and Hybrid Networking#AWS Client VPN\|VPC Connectivity and Hybrid Networking]] |
| Amazon CloudFront | Content delivery network | [[12 CloudFront and Global Accelerator#Amazon CloudFront\|CloudFront and Global Accelerator]] |
| AWS Direct Connect | Dedicated private link to AWS | [[10 VPC Connectivity and Hybrid Networking#AWS Direct Connect\|VPC Connectivity and Hybrid Networking]] |
| Elastic Load Balancing (ELB) | Distributes traffic across targets | [[05 Load Balancing and Auto Scaling#Elastic Load Balancing\|Load Balancing and Auto Scaling]] |
| AWS Global Accelerator | Static IPs and fast routing on the AWS network | [[12 CloudFront and Global Accelerator#AWS Global Accelerator\|CloudFront and Global Accelerator]] |
| AWS PrivateLink | Private access to a single service | [[10 VPC Connectivity and Hybrid Networking#AWS PrivateLink\|VPC Connectivity and Hybrid Networking]] |
| Amazon Route 53 | DNS and domain registration | [[11 Route 53#Amazon Route 53\|Route 53]] |
| AWS Site-to-Site VPN | IPsec link between a network and AWS | [[10 VPC Connectivity and Hybrid Networking#AWS Site-to-Site VPN\|VPC Connectivity and Hybrid Networking]] |
| AWS Transit Gateway | Central hub for VPCs and on-premises networks | [[10 VPC Connectivity and Hybrid Networking#AWS Transit Gateway\|VPC Connectivity and Hybrid Networking]] |
| Amazon VPC | Your private network on AWS | [[09 VPC Fundamentals#The big picture\|VPC Fundamentals]] |

### Security, Identity, and Compliance

| Service | What it does | Chapter |
| --- | --- | --- |
| AWS Artifact | AWS's compliance reports | [[24 Threat Protection and Security Services#AWS Artifact\|Threat Protection and Security Services]] |
| AWS Certificate Manager (ACM) | TLS certificates | [[23 Encryption and Secrets#AWS Certificate Manager\|Encryption and Secrets]] |
| AWS CloudHSM | Single-tenant hardware security modules | [[23 Encryption and Secrets#AWS CloudHSM\|Encryption and Secrets]] |
| Amazon Cognito | Sign-in for app users | [[02 IAM and Federation#Amazon Cognito\|IAM and Federation]] |
| Amazon Detective | Investigate the root cause of findings | [[24 Threat Protection and Security Services#Amazon Detective\|Threat Protection and Security Services]] |
| AWS Directory Service | Managed Active Directory options | [[02 IAM and Federation#AWS Directory Service\|IAM and Federation]] |
| AWS Firewall Manager | Security rules across an organisation | [[24 Threat Protection and Security Services#AWS Firewall Manager\|Threat Protection and Security Services]] |
| Amazon GuardDuty | Threat detection from logs | [[24 Threat Protection and Security Services#Amazon GuardDuty\|Threat Protection and Security Services]] |
| AWS IAM Identity Center | Workforce single sign-on | [[02 IAM and Federation#AWS IAM Identity Center\|IAM and Federation]] |
| Amazon Inspector | Vulnerability scanning | [[24 Threat Protection and Security Services#Amazon Inspector\|Threat Protection and Security Services]] |
| AWS KMS | Encryption keys | [[23 Encryption and Secrets#AWS KMS\|Encryption and Secrets]] |
| Amazon Macie | Finds sensitive data in S3 | [[24 Threat Protection and Security Services#Amazon Macie\|Threat Protection and Security Services]] |
| AWS Network Firewall | Managed firewall for VPCs | [[09 VPC Fundamentals#AWS Network Firewall\|VPC Fundamentals]] |
| AWS Resource Access Manager (AWS RAM) | Shares resources between accounts | [[03 Multi-Account Governance#AWS Resource Access Manager\|Multi-Account Governance]] |
| AWS Secrets Manager | Stores and rotates secrets | [[23 Encryption and Secrets#AWS Secrets Manager\|Encryption and Secrets]] |
| AWS Security Hub | One view of security findings | [[24 Threat Protection and Security Services#AWS Security Hub\|Threat Protection and Security Services]] |
| AWS Shield | DDoS protection | [[24 Threat Protection and Security Services#AWS Shield\|Threat Protection and Security Services]] |
| AWS WAF | Web application firewall | [[24 Threat Protection and Security Services#AWS WAF\|Threat Protection and Security Services]] |
| IAM | Identities and permissions | [[02 IAM and Federation#IAM in one minute\|IAM and Federation]] |

### Serverless

| Service | What it does | Chapter |
| --- | --- | --- |
| AWS Fargate | Serverless containers | [[18 Containers#AWS Fargate\|Containers]] |
| AWS Lambda | Serverless functions | [[16 Lambda and Serverless#AWS Lambda\|Lambda and Serverless]] |

### Storage

| Service | What it does | Chapter |
| --- | --- | --- |
| AWS Backup | Central backup service | [[28 High Availability and Disaster Recovery#AWS Backup\|High Availability and Disaster Recovery]] |
| Amazon EBS | Block storage for EC2 | [[08 Block and File Storage#Amazon EBS\|Block and File Storage]] |
| Amazon EFS | Managed NFS file system | [[08 Block and File Storage#Amazon EFS\|Block and File Storage]] |
| Amazon FSx (for all types) | Managed third-party file systems | [[08 Block and File Storage#Amazon FSx\|Block and File Storage]] |
| Amazon S3 | Object storage | [[06 Amazon S3#The basics\|Amazon S3]] |
| Amazon S3 Glacier | Archive storage classes | [[06 Amazon S3#Storage classes\|Amazon S3]] |
| AWS Storage Gateway | On-premises access to cloud storage | [[27 Migration and Data Transfer#AWS Storage Gateway\|Migration and Data Transfer]] |

## Out-of-scope services

AWS's published list. These should not appear as correct answers, so an option that names one is probably a distractor. AWS says that this list is non-exhaustive too.

- **Application Integration:** Amazon Managed Workflows for Apache Airflow (Amazon MWAA)
- **Compute:** Amazon Lightsail
- **Database:** Amazon RDS on VMware
- **Developer Tools:** AWS CDK, AWS CloudShell, AWS CodeArtifact, AWS CodeBuild, AWS CodeCommit, AWS CodeDeploy, Amazon Corretto, AWS Fault Injection Simulator (AWS FIS), AWS Tools and SDKs
- **Front-End Web and Mobile:** Amazon Location Service
- **Game Tech:** Amazon GameLift
- **Internet of Things:** All services
- **Machine Learning:** Apache MXNet on AWS, AWS Deep Learning AMIs (DLAMI), AWS Deep Learning Containers, Amazon HealthLake, AWS Inferentia, Amazon Personalize, PyTorch on AWS, TensorFlow on AWS
- **Management and Governance:** AWS Console Mobile Application, AWS Distro for OpenTelemetry
- **Media Services:** AWS Elemental Appliances and Software, AWS Elemental MediaConnect, AWS Elemental MediaConvert, AWS Elemental MediaLive, AWS Elemental MediaPackage, AWS Elemental MediaTailor, Amazon Interactive Video Service (Amazon IVS)
- **Migration and Transfer:** Migration Evaluator
- **Networking and Content Delivery:** AWS Cloud Map
- **Quantum Technologies:** Amazon Braket
- **Satellite:** AWS Ground Station

**AWS Cloud Map** deserves a word, because it sometimes appears in architectures. It is a service discovery directory that tracks the location and health of application resources.

## Services on neither list

The in-scope list is non-exhaustive, so these may still appear. The chapters cover them as background: Amazon Timestream, Amazon MemoryDB, Amazon SES, AWS Trusted Advisor, AWS AppSync, AWS Elastic Disaster Recovery, AWS Cost Anomaly Detection, AWS Pricing Calculator, Amazon VPC Lattice, and Amazon Managed Service for Apache Flink.

---
**Home:** [[Home]]
