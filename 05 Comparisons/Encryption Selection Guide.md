---
tags: [comparison, scope/in]
---

# Encryption Selection Guide

| Need | Use |
| --- | --- |
| Simple default for [[Amazon S3\|S3]] | [[S3 Encryption\|SSE-S3]] |
| Audit key use, control rotation | SSE-KMS |
| Reduce [[AWS KMS\|KMS]] calls | S3 Bucket Key |
| Two layers of encryption | DSSE-KMS |
| AWS must never see plaintext | Client-side encryption |
| Single-tenant HSM | [[AWS CloudHSM]] |
| Keys kept outside AWS | [[KMS Custom Key Stores|External Key Store]] |
| Same key across Regions | [[KMS Multi-Region Keys]] |
| TLS certificates | [[AWS Certificate Manager]] |

## Exam tasks
- [[Task 1.3 Determine appropriate data security controls]]

---
**Up:** [[Decision Guides Map]]
