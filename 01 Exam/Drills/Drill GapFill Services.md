---
tags: [drill, scope/in]
---

# Drill GapFill Services

Adapted from [RonitSachdev/aws-saa-c03-guides](https://github.com/RonitSachdev/aws-saa-c03-guides) (CC BY 4.0), with outdated facts changed.

## Question patterns

- *"Existing on-prem app uses RabbitMQ with AMQP; migrate with minimal code changes"* → **[[Amazon MQ]]** (protocol keywords = MQ; [[Amazon SQS|SQS]] would mean rewriting)
- *"HTTPS on [[Amazon CloudFront|CloudFront]] with a custom domain — where's the certificate?"* → **[[AWS Certificate Manager|ACM]] in us-east-1** (CloudFront only reads certs from N. Virginia)
- *"IPv6-only instances need outbound internet access but must block inbound"* → **Egress-only [[Internet Gateway and Route Tables|Internet Gateway]]** (the [[IPv6 in a VPC|IPv6]] answer; [[NAT Gateways|NAT gateway]] is IPv4)
- *"Automatically extract fields and tables from scanned invoices"* → **[[Amazon Textract|Textract]]** (forms/documents, beyond OCR — not [[Amazon Rekognition|Rekognition]])
- *"Migrate a self-managed Apache Kafka cluster with no application changes"* → **[[Amazon MSK|MSK]]** (the word Kafka does all the work)
- *"Mobile app needs a GraphQL API with real-time data sync"* → **[[AWS AppSync|AppSync]]** (GraphQL/subscriptions/offline = AppSync every time)
- *"Automatically apply OS security patches to 500 [[Amazon EC2|EC2 instances]] monthly"* → **[[SSM Patch Manager]]** (fleet patching on a schedule)
- *"Encrypt all existing objects already stored in an [[Amazon S3|S3 bucket]]"* → **S3 Batch Operations** (default encryption only covers new objects)
- *"Data team needs managed Apache Spark for nightly processing at low cost"* → **EMR with Spot task nodes** (Spark = EMR; Spot = cheap)
- *"Regulations require workloads to run in the company's own datacenter using AWS services"* → **Outposts** (AWS racks on your floor — data residency)
- *"Shell access to private instances without SSH keys or bastion hosts"* → **SSM Session Manager** (no port 22, fully audited)
- *"Migrate Oracle to Aurora PostgreSQL"* → **DMS + SCT** (different engines = heterogeneous = add the Schema Conversion Tool)

## Pocket card

| Keyword | Answer |
|---|---|
| MQTT / AMQP / JMS, minimal rewrite | Amazon MQ |
| Lift-and-shift servers (rehost) | MGN |
| DR replication, RPO seconds | Elastic Disaster Recovery (DRS) |
| DB migration, different engines | DMS + SCT |
| Free auto-renewing TLS certs | ACM |
| CloudFront certificate region | us-east-1 (always) |
| IPv6 outbound-only | Egress-only Internet Gateway |
| On-prem → VPC DNS | Resolver inbound endpoint |
| VPC → on-prem DNS | Resolver outbound endpoint |
| AWS racks in your datacenter | Outposts |
| Single-digit ms to a metro city | Local Zones |
| 5G edge | Wavelength |
| Serverless ETL + catalog | Glue |
| Spark / Hadoop | EMR |
| Kafka | MSK |
| BI dashboards | Amazon Quick |
| Data lake + fine-grained access | Lake Formation |
| SaaS → S3 | AppFlow |
| Images/video analysis | Rekognition |
| Speech → text / text → speech | Transcribe / Polly |
| Sentiment | Comprehend |
| Scanned forms/invoices | Textract |
| Intelligent doc search | Kendra |
| Recommendations / forecasts / chatbots | Personalize / Forecast / Lex |
| Custom ML | SageMaker |
| No-SSH access / fleet scripts / auto-patching | Session Manager / Run Command / Patch Manager |
| Batch jobs > 15 min, Docker | AWS Batch |
| GraphQL, offline sync | AppSync |
| Full-stack quickstart | Amplify |
| Application emails | SES |
| Bulk ops on existing S3 objects | S3 Batch Operations |
| Instant prod DB copy for testing | Aurora cloning |
| Distributed tracing | X-Ray |
| Compliance reports for auditors | AWS Artifact |

---
**Up:** [[Drills Map]]
