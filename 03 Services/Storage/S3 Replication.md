---
tags: [service, cat/storage, scope/in]
aliases: ["Cross-Region Replication", "CRR", "SRR"]
---

# S3 Replication

To perform replication we must enable versioning in source and destination buckets. Buckets can be in different AWS accounts. Copying is asynchronous and we must give proper [[AWS IAM|IAM]] permissions to [[Amazon S3|S3]].

- **Cross-Region Replication (CRR)** - replicates objects between buckets in different AWS regions. It’s useful for [[Disaster Recovery Strategies|disaster recovery]], latency reduction and compliance.
- **Same-Region Replication (SRR)** - replicates objects between buckets within the same AWS region. It’s useful for log aggregation and live replication between production and test accounts.

- **One-way Replication** - replicate objects from a source bucket to a destination bucket, but not back to the source.
- **Two-way Replication** - allows for bi-directional **syncing** between two S3 buckets. Changes made in either bucket can be reflected in the other.

Unencrypted objects and objects encrypted with [[S3 Encryption|SSE-S3]] are replicated by default. Object encrypted with SSE-C can also be replicated.

For objects encrypted with SSE-KMS, we need to enable the option:

1. Specify which [[AWS KMS|KMS]] Key to encrypt the objects within the target bucket.
2. Adapt the KMS Key Policy for the target key.
3. Create IAM Role with kms:Decrypt for the source KMS Key and kms:Encrypt for the target KMS Key.

We can use [[KMS Multi-Region Keys|MRK]], but they are currently treated as independent keys by S3 (**the object will still be decrypted and then encrypted**).

Only new objects replicate. Use **S3 Batch Replication** for existing ones. **S3 Replication Time Control** replicates 99.9% of objects within 15 minutes. Delete markers can optionally replicate, but version deletions don't.

## Exam tasks
- [[Task 1.3 Determine appropriate data security controls]]

---
**Up:** [[Amazon S3]] · **Map:** [[Storage Map]]
