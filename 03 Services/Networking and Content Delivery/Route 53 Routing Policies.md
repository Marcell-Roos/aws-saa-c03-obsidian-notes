---
tags: [service, cat/networking, scope/in]
aliases: ["routing policy", "Routing Policy"]
---

# Route 53 Routing Policies

| Policy | Use it for | Health checks |
| --- | --- | --- |
| Simple | One resource | No |
| Weighted | Percentage split, canary | Yes |
| Latency | Lowest latency Region | Yes |
| Failover | Active-passive DR | Yes, required on primary |
| [[Route 53 Geolocation Routing\|Geolocation]] | By user's country or continent | Yes |
| [[Route 53 Geoproximity Routing\|Geoproximity]] | By distance, with bias | Yes |
| IP-based | By client [[CIDR and IP Addressing\|CIDR]] | Yes |
| Multivalue | Up to 8 healthy records | Yes |

```mermaid
flowchart TD
    Q{"What decides the answer?"}
    Q -->|"Percentage"| W["Weighted"]
    Q -->|"Speed"| L["Latency"]
    Q -->|"Primary down"| F["Failover"]
    Q -->|"Country rules"| G["Geolocation"]
    Q -->|"Distance and bias"| P["Geoproximity"]
    Q -->|"Client IP range"| I["IP-based"]
```

## In this topic
- [[Route 53 Failover Routing]]
- [[Route 53 Geolocation Routing]]
- [[Route 53 Geoproximity Routing]]
- [[Route 53 IP-based Routing]]
- [[Route 53 Latency Routing]]
- [[Route 53 Multivalue Routing]]
- [[Route 53 Simple Routing]]
- [[Route 53 Weighted Routing]]

## Exam tasks
- [[Task 2.2 Design highly available and or or fault-tolerant architectures]]

---
**Up:** [[Amazon Route 53]] · **Map:** [[Networking and Content Delivery Map]]
