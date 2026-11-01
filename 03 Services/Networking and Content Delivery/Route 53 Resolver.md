---
tags: [service, cat/networking, scope/in]
aliases: ["Resolver endpoints"]
---

# Route 53 Resolver

Provides [[DNS Fundamentals|DNS]] in a [[Amazon VPC|VPC]] and connects it with on-premises DNS.

- **Inbound endpoint:** on-premises servers resolve names in AWS.
- **Outbound endpoint:** VPC resources resolve on-premises names through forwarding rules.

Rules can be shared with [[AWS Resource Access Manager]].

```mermaid
flowchart LR
    OP["On-premises DNS"] -->|"Inbound endpoint"| R["Route 53 Resolver"]
    R -->|"Outbound endpoint"| OP
    V["VPC resources"] --> R
```

## Exam tasks
- [[Task 3.4 Determine high-performing and or or scalable network architectures]]

---
**Up:** [[Amazon Route 53]] · **Map:** [[Networking and Content Delivery Map]]
