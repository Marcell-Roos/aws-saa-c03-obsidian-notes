---
tags: [service, cat/networking, scope/in]
aliases: ["PrivateLink"]
---

# AWS PrivateLink

**AWS PrivateLink** allows us to privately access services hosted on AWS, including our own applications, third-party services, and AWS services, without exposing our traffic to the public internet. It simplifies the network architecture, improves security. Does not require [[Amazon VPC|VPC]] peering, internet gateway, NAT, [[Internet Gateway and Route Tables|route tables]], but it requires a [[Network Load Balancer|NLB]] on service VPC and [[Elastic Network Interface|ENI]] on customer VPC.

## Exam tasks
- [[Task 1.2 Design secure workloads and applications]]
- [[Task 3.4 Determine high-performing and or or scalable network architectures]]

---
**Up:** [[Amazon VPC]] · **Map:** [[Networking and Content Delivery Map]]
