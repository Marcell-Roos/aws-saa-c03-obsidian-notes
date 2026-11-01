---
tags: [comparison, scope/in]
---

# EBS vs EFS vs S3

| | [[Amazon EBS]] | [[Amazon EFS]] | [[Amazon S3]] |
| --- | --- | --- | --- |
| Type | Block | File (NFS) | Object |
| Attach | One instance, or [[EBS Multi-Attach\|Multi-Attach]] in one AZ | Thousands of Linux clients across AZs | HTTP API |
| Scope | AZ | Region, or One Zone | Region |
| Scaling | Manual resize | Automatic | Automatic |
| Pricing | Provisioned GB | Used GB | Used GB + requests |
| Use | Boot, databases | Shared files, CMS | Backups, [[Data Lakes\|data lakes]], static sites |

---
**Up:** [[Comparisons Map]]
