---
tags: [comparison, scope/in]
---

# Data Transfer Selection Guide

| Situation | Use |
| --- | --- |
| Small data, spare bandwidth | Internet or [[AWS Site-to-Site VPN]] |
| Large, repeated transfers | [[AWS Direct Connect]] |
| Scheduled file sync | [[AWS DataSync]] |
| Databases | [[AWS DMS]] |
| Global uploads to [[Amazon S3\|S3]] | [[S3 Performance|S3 Transfer Acceleration]] |
| Network would take over a week | [[AWS Snow Family]] (existing customers) |

Quick check: 100 TB over a 1 Gbps line at full speed takes about 9 days.

## Exam tasks
- [[Task 3.5 Determine high-performing data ingestion and transformation solutions]]

---
**Up:** [[Decision Guides Map]]
