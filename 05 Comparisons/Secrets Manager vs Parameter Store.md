---
tags: [comparison, scope/in]
---

# Secrets Manager vs Parameter Store

| | [[AWS Secrets Manager]] | [[SSM Parameter Store]] |
| --- | --- | --- |
| Purpose | Secrets | Config and secrets |
| Automatic rotation | Yes, built in with [[AWS Lambda\|Lambda]] | No native rotation |
| Cost | Per secret | Standard tier free |
| Cross-Region replication | Yes | No |
| Pick for | Database credentials that rotate | App config and low-cost strings |

---
**Up:** [[Comparisons Map]]
