---
tags: [service, cat/networking, scope/in]
---

# VPC Peering

**VPC Peering** connects two [[Amazon VPC|VPCs]] privately using AWS network. It makes two VPCs behave as if they were in the same network. They must not have overlapping [[CIDR and IP Addressing|CIDR]] (IP address range).

VPC Peering connection is not transitive (must be established for each VPC that need to communicate with one another).

We must update [[Internet Gateway and Route Tables|route tables]] in each VPC’s subnets to ensure [[Amazon EC2|EC2 instances]] can communicate with each other. We can create VPC Peering connection between VPCs in different AWS accounts/regions. Also we can reference a [[Security Groups|security group]] in a peered VPC (works cross accounts in same region).

## Exam tasks
- [[Task 3.4 Determine high-performing and or or scalable network architectures]]
- [[Task 4.4 Design cost-optimized network architectures]]

---
**Up:** [[Amazon VPC]] · **Map:** [[Networking and Content Delivery Map]]
