---
tags: [comparison, scope/in]
---

# NAT Instance vs NAT Gateway

The source had this only as an image.

| | [[NAT Gateways|NAT Gateway]] | [[NAT Instances|NAT Instance]] |
| --- | --- | --- |
| Managed | Yes | No, you patch it |
| Availability | Within an AZ, or regional mode across AZs | Needs your own failover script or [[Amazon EC2 Auto Scaling\|ASG]] |
| Bandwidth | Scales automatically | Depends on instance type |
| Security groups | Not attachable | Yes |
| Bastion use | No | Yes |
| Cost | Hourly + per GB | Instance cost |
| Setup | Nothing extra | Disable source/destination check |

## Exam tasks
- [[Task 4.4 Design cost-optimized network architectures]]

---
**Up:** [[Comparisons Map]]
