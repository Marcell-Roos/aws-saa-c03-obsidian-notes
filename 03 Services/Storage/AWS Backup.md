---
tags: [service, cat/storage, scope/in]
aliases: ["Backup Vault Lock"]
---

# AWS Backup

**AWS Backup** is a fully-managed service to centrally manage and automate backups across AWS services. It can have on-demand and scheduled backups. Supports [[DynamoDB Backups and S3 Integration|PITR]].

**Cross-Region Backup** - backing up data from one AWS region to another. This is useful for [[Disaster Recovery Strategies|disaster recovery]] scenarios where we want to ensure data availability even if an entire AWS region becomes unavailable due to a disaster or outage.

**Cross-Account Backup** - backing up data from AWS resources in one AWS account to AWS Backup vaults in another AWS account. This is useful for scenarios where we want to centralize backups for multiple AWS accounts in a single backup location.

**Backup Vault Lock** - enforces WORM state for all the backups that we store in our AWS Backup Vault. It is additional layer of defense to protect our backups against inadvertent or malicious delete operations. In **compliance mode** not even the root user can delete backups once the grace period ends. In **governance mode**, users with sufficient [[AWS IAM|IAM]] permissions can remove the lock.

**Logically air-gapped vaults** add isolation and can be shared across accounts for recovery. Backup Vault Lock has a **grace time** during which compliance mode can still be removed.

## Exam tasks
- [[Task 1.3 Determine appropriate data security controls]]
- [[Task 2.2 Design highly available and or or fault-tolerant architectures]]
- [[Task 4.1 Design cost-optimized storage solutions]]

---
**Map:** [[Storage Map]]
