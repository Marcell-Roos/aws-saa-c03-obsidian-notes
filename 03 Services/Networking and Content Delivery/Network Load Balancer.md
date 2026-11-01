---
tags: [service, cat/networking, scope/in]
aliases: ["NLB", "NLBs"]
---

# Network Load Balancer

**NLB** operates at transport layer (Layer 4). Can handle high volumes of traffic with ultra-low latency, making it suitable for applications that require extreme performance, low latency, and TCP/UDP-level traffic handling. A listener can forward to multiple target groups using weights from 0 to 999.

NLB has **one static IP per AZ** and supports assigning Elastic IP (helpful for whitelisting specific IP).

**Target Groups**:

- **[[Amazon EC2|EC2 Instances]]**.
- **IP Addresses** (must be private IPs).
- **[[Application Load Balancer|ALB]].**

Health checks support the TCP, HTTP and HTTPS protocols.

If we specify targets using an instance ID, traffic is routed to instances using the primary private IP address specified in the primary network interface for the instance.

---
**Up:** [[Elastic Load Balancing]] · **Map:** [[Networking and Content Delivery Map]]
