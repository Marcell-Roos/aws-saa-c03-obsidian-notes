---
tags: [service, cat/management, scope/in]
aliases: ["Config Rules", "Config rules"]
---

# AWS Config

**AWS Config** helps us with auditing and recording compliance of our AWS resources. It can record configurations and changes over time. It is possible to store the configuration data into [[Amazon S3|S3]] (analyzed by [[Amazon Athena|Athena]]).

Questions that can be solved by AWS Config:

- Is there unrestricted SSH access to my [[Security Groups|security groups]]?
- Do my buckets have any public access?
- How has my [[Application Load Balancer|ALB]] configuration changed over time?

Config is a per-region service and can be aggregated across regions and accounts. We can receive alerts ([[Amazon SNS|SNS]] notifications) for any changes.

**Config Rules**

We can use AWS managed config rules or make custom config rules (written as **[[AWS Lambda|Lambda functions]]** or as **Guard** custom policy rules). Rules can be evaluated/triggered for each config change and/or at regular time intervals.

Config Rules does not prevent actions from happening (**no deny**).

**Config Remediations**

We can automate remediation of non-compliant resource using [[SSM Automation]] Documents. It is possible to create custom Automation Documents that invokes Lambda function.

We can set Remediation Retries if the resource is still non-compliant after auto-remediation.

**Config Notifications**

We can use [[Amazon EventBridge|EventBridge]] to trigger notifications when AWS resources are non-compliant.

There is ability to send configuration changes and compliance state notifications to SNS.

Config is regional, charged per item recorded, and it detects rather than prevents. Remediation runs through SSM Automation.

## In this topic
- [[Config Conformance Packs]]

## Exam tasks
- [[Task 1.3 Determine appropriate data security controls]]

---
**Map:** [[Management and Governance Map]]
