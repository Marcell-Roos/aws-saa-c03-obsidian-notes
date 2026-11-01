---
tags: [service, cat/networking, scope/in]
aliases: ["Internet Gateway", "route table", "route tables", "Route Tables", "IGW"]
---

# Internet Gateway and Route Tables

**Internet Gateway** is a horizontally scaled, redundant, and highly available [[Amazon VPC|VPC]] component that allows instances within our VPC to connect to the internet, and for the internet to initiate connections with instances within our VPC (if allowed by security rules).

One VPC can only be attached to one IGW and vice versa.

**Routing Table** is a set of rules (routes) that determine where network traffic is directed. Every subnet in our VPC must be associated with a route table.

## Exam tasks
- [[Task 1.2 Design secure workloads and applications]]

---
**Up:** [[Amazon VPC]] · **Map:** [[Networking and Content Delivery Map]]
