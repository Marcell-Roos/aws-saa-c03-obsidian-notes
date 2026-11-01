---
tags: [concept, scope/in]
aliases: ["encryption at rest", "encryption in transit"]
---

# Encryption at Rest and in Transit

- **At rest:** [[AWS KMS]] backs encryption for [[Amazon EBS]], [[Amazon S3]], [[Amazon RDS]], [[Amazon DynamoDB]] and others.
- **In transit:** TLS, with certificates from [[AWS Certificate Manager]].
- **Client-side:** the application encrypts before sending, so AWS only sees ciphertext.

To enforce HTTPS on [[Amazon S3|S3]], deny requests where `aws:SecureTransport` is false. An unencrypted [[Amazon RDS|RDS]] or [[Amazon EBS|EBS volume]] can't be encrypted in place, so copy a snapshot with encryption and restore it.

## Exam tasks
- [[Task 1.3 Determine appropriate data security controls]]

---
**Up:** [[Concepts Map]]
