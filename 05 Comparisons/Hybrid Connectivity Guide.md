---
tags: [comparison, scope/in]
---

# Hybrid Connectivity Guide

```mermaid
flowchart TD
    Q{"Requirement?"}
    Q -->|"Fast setup, encrypted"| V["Site-to-Site VPN"]
    Q -->|"Consistent high bandwidth"| D["Direct Connect"]
    Q -->|"Private and encrypted line"| DV["Direct Connect + VPN"]
    Q -->|"Backup for Direct Connect"| B["VPN or second Direct Connect"]
    Q -->|"Many VPCs and sites"| T["Transit Gateway"]
    Q -->|"Multiple Regions over Direct Connect"| G["Direct Connect Gateway"]
    Q -->|"Individual users"| C["Client VPN"]
```

Resilient [[AWS Direct Connect|Direct Connect]]: two connections at two locations for high resiliency, or two at each for maximum resiliency.

## Exam tasks
- [[Task 3.4 Determine high-performing and or or scalable network architectures]]

---
**Up:** [[Decision Guides Map]]
