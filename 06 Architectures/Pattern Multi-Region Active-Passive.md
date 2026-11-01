---
tags: [architecture, scope/in]
---

# Pattern Multi-Region Active-Passive

```mermaid
flowchart TB
    R["Route 53 failover + health check"]
    R --> P["Primary Region: ALB, ASG, Aurora writer"]
    R -.-> S["DR Region: ALB, small ASG, Aurora reader"]
    P -->|"Aurora Global Database"| S
    P -->|"S3 Cross-Region Replication"| S
```

See [[Disaster Recovery Strategies]].

## Exam tasks
- [[Task 2.2 Design highly available and or or fault-tolerant architectures]]

---
**Up:** [[Architecture Patterns]]
