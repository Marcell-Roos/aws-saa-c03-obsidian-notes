---
tags: [service, cat/networking, scope/in]
aliases: ["NAT Gateway", "NAT gateway"]
---

# NAT Gateways

**NAT Gateway** is AWS managed NAT with higher bandwidth, [[Scalability and High Availability|high availability]] and no administration. We pay per hour for usage and bandwidth. A classic (zonal) NAT Gateway is created in a specific AZ and uses an Elastic IP. A **regional NAT Gateway** spans AZs automatically and needs no public [[Amazon VPC|subnet]].

It can't be used by [[Amazon EC2|EC2 instance]] in the same subnet (only from other subnets). It requires an [[Internet Gateway and Route Tables|Internet Gateway]].

A zonal NAT Gateway is resilient within a single AZ. We must create multiple NAT Gateways in multiple AZs for fault-tolerance. There is no cross-AZ failover needed because if an AZ goes down it doesn't need NAT.

Regional mode needs no public subnet and no per-AZ route tables. A zonal gateway can't be used by instances in its own subnet. See [[NAT Instance vs NAT Gateway]].

## Exam tasks
- [[Task 1.2 Design secure workloads and applications]]
- [[Task 4.4 Design cost-optimized network architectures]]

---
**Up:** [[Amazon VPC]] · **Map:** [[Networking and Content Delivery Map]]
