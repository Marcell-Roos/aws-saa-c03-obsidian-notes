---
tags: [service, cat/storage, scope/in]
---

# EBS Encryption

When we create an encrypted [[Amazon EBS|EBS volume]]:

- Data at rest is encrypted inside the volume.
- All the data in flight moving between the instance and the volume is encrypted.
- All snapshots are encrypted.
- All volumes created from the snapshot are encrypted.

Encryption has a minimal impact on latency. EBS encryption leverages keys from [[AWS KMS|KMS]] (AES-256).

## Exam tasks
- [[Task 1.3 Determine appropriate data security controls]]

---
**Up:** [[Amazon EBS]] · **Map:** [[Storage Map]]
