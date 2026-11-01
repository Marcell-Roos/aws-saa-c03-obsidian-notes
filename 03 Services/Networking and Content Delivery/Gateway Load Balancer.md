---
tags: [service, cat/networking, scope/in]
aliases: ["GWLB"]
---

# Gateway Load Balancer

**GWLB** operates at network layer (Layer 3). It routes traffic based on IP addresses and supports both IPv4 and [[IPv6 in a VPC|IPv6]]. This makes it highly efficient for managing network traffic and distributing it across multiple network appliances.

GWLB combines following functions:

- Transparent Network Gateway - routes traffic without changing the source or destination IP addresses (**bump-in-the-wire**). It provides a single point of entry for all network traffic.
- Load Balancer - distributes traffic to our virtual appliances.

It uses the GENEVE protocol on port 6081.

**Target Groups**:

- **[[Amazon EC2|EC2 Instances]]**.
- **IP Addresses** (must be private IPs).

---
**Up:** [[Elastic Load Balancing]] · **Map:** [[Networking and Content Delivery Map]]
