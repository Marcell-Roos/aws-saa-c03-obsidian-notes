---
tags: [comparison, scope/in]
---

# KMS vs CloudHSM

| | [[AWS KMS]] | [[AWS CloudHSM]] |
| --- | --- | --- |
| Tenancy | Multi-tenant managed service | Single-tenant HSM in your [[Amazon VPC\|VPC]] |
| Who controls keys | AWS operates, you control use | You alone |
| FIPS | 140-3 Level 3 HSMs | 140-2 or 140-3 Level 3 in FIPS mode |
| Integration | Most AWS services | Custom key store, or your apps |
| Effort | Low | High: you run the cluster |

The old rule "Level 3 means [[AWS CloudHSM|CloudHSM]]" no longer separates them. Look for **single-tenant** or **exclusive control**.

---
**Up:** [[Comparisons Map]]
