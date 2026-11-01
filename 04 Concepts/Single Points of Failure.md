---
tags: [concept, scope/in]
aliases: ["single point of failure"]
---

# Single Points of Failure

Check each layer for one thing whose loss stops the workload.

| Layer | Fix |
| --- | --- |
| One instance | [[Amazon EC2 Auto Scaling]] across AZs behind a [[Elastic Load Balancing\|load balancer]] |
| One database | [[RDS Multi-AZ]] or [[Amazon Aurora]] |
| One [[NAT Gateways\|NAT Gateway]] | One per AZ, or a regional NAT Gateway. See [[NAT Gateways]] |
| One VPN or [[AWS Direct Connect\|Direct Connect]] link | Second link, or a VPN backup |
| One Region | [[Disaster Recovery Strategies]] |

## Exam tasks
- [[Task 2.2 Design highly available and or or fault-tolerant architectures]]

---
**Up:** [[Concepts Map]]
