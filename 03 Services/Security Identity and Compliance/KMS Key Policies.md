---
tags: [service, cat/security, scope/in]
---

# KMS Key Policies

**KMS Key Policies** - control access to [[AWS KMS|KMS keys]] (similar to [[S3 Access Control|S3 bucket policies]]).

- **Default KMS Key Policy** - created if we don't provide a specific KMS Key Policy. Root user has complete access to the key.
- **Custom KMS Key Policy** - define users, roles that can access the KMS key and who can administer the key. Useful for [[Cross-Account Access|cross-account access]] of our KMS key.

To copy snapshot across accounts we need to create a snapshot encrypted with our own KMS key. Then attach a KMS Key Policy to authorize cross-account access and share the encrypted snapshot. In target account we need to create a copy of the snapshot, encrypt it with CMK in our account and then create a volume from snapshot.

## Exam tasks
- [[Task 1.3 Determine appropriate data security controls]]

---
**Up:** [[AWS KMS]] · **Map:** [[Security Identity and Compliance Map]]
