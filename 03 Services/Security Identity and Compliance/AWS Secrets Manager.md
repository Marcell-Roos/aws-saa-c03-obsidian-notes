---
tags: [service, cat/security, scope/in]
aliases: ["Secrets Manager"]
---

# AWS Secrets Manager

**ASM** is a newer service which is used for storing secrets. It has capability to force rotation of secrets every X days. We can automate generation of secrets on rotation using [[AWS Lambda|Lambda]]. All secrets are encrypted using [[AWS KMS|KMS]].

Can be integrated with [[Amazon RDS]] (MySQL, Postgres, [[Amazon Aurora|Aurora]]). Mostly meant for RDS integration.

We can replicate secrets across multiple regions. Secrets Manager keeps [[RDS Read Replicas|read replicas]] in sync with the primary secret. There is an ability to promote a read replica secret to a standalone secret.

Use cases: multi-region apps, [[Disaster Recovery Strategies|disaster recovery]] strategies, multi-region databases…

## Exam tasks
- [[Task 1.2 Design secure workloads and applications]]

---
**Map:** [[Security Identity and Compliance Map]]
