---
tags: [service, cat/networking, scope/in]
---

# Egress-Only Internet Gateway

**Egress-Only Internet Gateway** is used for [[IPv6 in a VPC|IPv6]] only (similar to a [[NAT Gateways|NAT Gateway]] but for IPv6). It allows outbound connections over IPv6 for instances in our [[Amazon VPC|VPC]] while preventing the internet to initiate an IPv6 connection to our instances. We must update the [[Internet Gateway and Route Tables|route tables]].

**IPv6 Routing**

In a private subnet, route `::/0` to the egress-only internet gateway. In a public subnet, route `::/0` to the internet gateway.

---
**Up:** [[Amazon VPC]] · **Map:** [[Networking and Content Delivery Map]]
