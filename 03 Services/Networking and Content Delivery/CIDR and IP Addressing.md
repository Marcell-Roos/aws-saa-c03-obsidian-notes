---
tags: [service, cat/networking, scope/in]
aliases: ["CIDR"]
---

# CIDR and IP Addressing

**CIDR (Classless Inter’Domain Routing)** - a method for allocating IP addresses. It is used in [[Security Groups]] rules and AWS networking in general. It help to define an IP address range.

CIDR consists of two components:

- **Base IP** - represents an IP contained in the range.
- **Subnet Mask** - defines how many bits can change in the IP.

**Private IP** addresses are used within a [[Amazon VPC|VPC]] and are not routable over the internet. They are used for internal communication between resources within the same VPC or between different VPCs if they are peered or connected via a VPN.

**Public IP** addresses are routable over the internet. They are used to allow resources to communicate with external networks and to be accessible from the internet.

## Exam tasks
- [[Task 3.4 Determine high-performing and or or scalable network architectures]]

---
**Up:** [[Amazon VPC]] · **Map:** [[Networking and Content Delivery Map]]
