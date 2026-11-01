---
tags: [architecture, scope/in]
---

# Case Study WhatsTheTime App

Requirements:

- It allows people to know what time it is.
- We don't need a database.
- Start small and can accept downtime.
- We want to fully scale vertically and horizontally, no downtime.

The source's architecture was an image. It grows through these stages:

```mermaid
flowchart LR
    A["One EC2 + Elastic IP"] --> B["Bigger instance"] --> C["Many instances"] --> D["ALB + ASG"] --> E["Multi-AZ ASG + Route 53 Alias"]
```

---
**Up:** [[Architecture Patterns]]
