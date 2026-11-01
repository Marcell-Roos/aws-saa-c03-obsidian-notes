---
tags: [concept, scope/in]
aliases: ["multi-tier", "three-tier"]
---

# Multi-Tier Architecture

Separates presentation, application and data layers, each in its own [[Amazon VPC|subnets]] and scaled independently.

```mermaid
flowchart TB
    U["Users"] --> CF["CloudFront"]
    CF --> ALB["ALB in public subnets"]
    ALB --> APP["App tier ASG in private subnets"]
    APP --> C["ElastiCache"]
    APP --> DB["RDS Multi-AZ in private subnets"]
```

Each tier's [[Security Groups|security group]] allows traffic only from the tier above. See [[Case Study Clothes Store App]].

## Exam tasks
- [[Task 2.1 Design scalable and loosely coupled architectures]]

---
**Up:** [[Concepts Map]]
