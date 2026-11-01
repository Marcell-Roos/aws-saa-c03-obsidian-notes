---
tags: [service, cat/networking, scope/in]
aliases: ["Traffic Mirroring"]
---

# VPC Traffic Mirroring

We can capture the source traffic ([[Elastic Network Interface|ENIs]]) and target traffic (ENI or [[Network Load Balancer|NLB]]). It’s possible to capture all packets or capture the packets of our interest (optionally, truncate packets). Source and target can be in the same [[Amazon VPC|VPC]] or different VPCs ([[VPC Peering]]). Traffic mirror filters can't inspect the actual packet of the incoming and outgoing traffic. It is **primarily used for monitoring and analysis**.

---
**Up:** [[Amazon VPC]] · **Map:** [[Networking and Content Delivery Map]]
