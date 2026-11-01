---
tags: [service, cat/security, scope/in]
aliases: ["GuardDuty"]
---

# Amazon GuardDuty

**GuardDuty** is an intelligent threat discovery service which protects our AWS account. It uses ML algorithms, anomaly detection and 3rd party data. Focuses on real-time threat detection.

Input data can include:

- **[[AWS CloudTrail|CloudTrail]] Event Logs** - unusual API calls, unauthorized deployments.
- **[[VPC Flow Logs]]** - unusual internal traffic, unusual IP address.
- **[[DNS Fundamentals|DNS]] Logs** - compromised [[Amazon EC2|EC2 instances]] sending encoded data within DNS queries.
- **Optional Features** - [[Amazon EKS|EKS]] Audit Logs, [[Amazon RDS|RDS]] & [[Amazon Aurora|Aurora]], [[Amazon EBS|EBS]], [[AWS Lambda|Lambda]], [[Amazon S3|S3]] Data Events…

We can setup [[Amazon EventBridge|EventBridge]] rules to be notified in case of findings. EventBridge rules can target AWS Lambda or [[Amazon SNS|SNS]].

GuardDuty can protect us against CryptoCurrency attacks.

## Exam tasks
- [[Task 1.2 Design secure workloads and applications]]

---
**Map:** [[Security Identity and Compliance Map]]
