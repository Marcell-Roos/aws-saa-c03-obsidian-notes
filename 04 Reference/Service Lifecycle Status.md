---
tags: [reference, scope/in]
---

# Service Lifecycle Status

AWS can list a service on the exam while closing it to new customers. Learn what these services do, but do not choose them for new designs unless a question says that the company already uses them.

Source: AWS's [maintenance](https://docs.aws.amazon.com/general/latest/gr/maintenance_services.html), [sunset](https://docs.aws.amazon.com/general/latest/gr/sunset_services.html) and [full shutdown](https://docs.aws.amazon.com/general/latest/gr/full_shutdown_services.html) pages, read on 2 November 2026. Only services relevant to this exam are listed here.

## What the stages mean

| Stage | Meaning |
| --- | --- |
| **Maintenance** | Existing customers can keep using it. No new customers |
| **Sunset** | AWS has set an end of support date |
| **Shutdown** | The service has ended |

## Shut down

| Service | Date |
| --- | --- |
| AWS Server Migration Service | 1 April 2023 |
| Snowmobile | 14 March 2024 |
| AWS OpsWorks | 1 May 2024 |
| Amazon QLDB | 31 July 2025 |
| Snowball Edge 80 TB and GPU models | 12 November 2025 |
| Amazon Elastic Transcoder | 13 November 2025 |
| Application Discovery Service Discovery Connector | 17 November 2025 |
| Kinesis Data Analytics for SQL | 27 January 2026 |
| AWS Panorama | 20 May 2026 |
| Amazon Inspector Classic | 20 May 2026 |
| DMS Fleet Advisor | 20 May 2026 |

## Sunset

| Service | End of support |
| --- | --- |
| AWS App Mesh | 30 September 2026 |
| AWS Proton | 7 October 2026 |
| AWS WAF Classic | 7 October 2026 |
| Amazon Pinpoint | 30 October 2026 |
| RDS Custom for Oracle | 31 March 2027 |
| AWS Infrastructure Composer | 29 September 2027 |
| Amazon Managed Blockchain | 29 September 2027 |
| Amazon DevOps Guru | 29 September 2027 |

AWS Proton stays on the exam guide's in-scope list, even though its end of support date has passed.

## Maintenance: closed to new customers

| Service | Announced |
| --- | --- |
| S3 Select and Glacier Select | 25 July 2024 |
| Amazon Forecast | 29 July 2024 |
| FSx File Gateway | 28 October 2024 |
| Amazon Monitron | 31 October 2024 |
| Timestream for LiveAnalytics | 20 June 2025 |
| Application Discovery Service | 7 October 2025 |
| S3 Glacier direct vault access | 7 October 2025 |
| Snowball Edge Compute Optimized and Storage Optimized | 7 October 2025 |
| AWS Migration Hub | 7 November 2025 |
| S3 Object Lambda | 7 November 2025 |
| Systems Manager Incident Manager and Change Manager | 7 November 2025 |
| AWS App Runner | 31 March 2026 |
| AWS Audit Manager | 31 March 2026 |
| CloudTrail Lake | 31 March 2026 |
| AWS Glue Ray jobs | 31 March 2026 |
| Comprehend topic modeling, event detection and prompt safety classification | 31 March 2026 |
| Rekognition Streaming Events and batch image content moderation | 31 March 2026 |
| Application Recovery Controller readiness check | 31 March 2026 |
| SNS message data protection | 31 March 2026 |
| Amazon Kendra | 30 June 2026 |
| Simple AD | 30 June 2026 |
| Amazon Cognito Sync | 30 June 2026 |

The AWS Storage Gateway Hardware Appliance is not on these pages either, but the Storage Gateway documentation says that it has not been offered since 12 May 2025, with support for existing customers until May 2028.

AWS Data Pipeline is not on these lifecycle pages, but its own documentation says that it is in maintenance mode and closed to new customers. It stays on the exam's in-scope list.

Several of these remain on the in-scope list too, including Snow Family, Application Discovery Service and Amazon S3 Glacier.

## Renamed

| Old | New |
| --- | --- |
| Kinesis Data Firehose | Amazon Data Firehose |
| Kinesis Data Analytics for Apache Flink | Amazon Managed Service for Apache Flink |
| QuickSight | Amazon Quick, with Quick Sight as its BI part |
| AWS Single Sign-On | AWS IAM Identity Center |
| SageMaker | Amazon SageMaker AI |
| Performance Insights | CloudWatch Database Insights |
| Control Tower guardrails | Controls |
| Security Hub | AWS Security Hub CSPM. The exam guide still says AWS Security Hub |
| Application Composer | AWS Infrastructure Composer |
| Application Migration Service | AWS Transform MGN. The exam guide still says AWS Application Migration Service |

---
**Home:** [[Home]]
