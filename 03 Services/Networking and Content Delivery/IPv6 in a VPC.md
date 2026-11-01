---
tags: [service, cat/networking, scope/in]
aliases: ["IPv6"]
---

# IPv6 in a VPC

Every IPv6 address in AWS is public and Internet-routable (no private range). IPv4 cannot be disabled for our [[Amazon VPC|VPC]] and subnets. We can enable IPv6 to operate in **dual-stack mode**. Our [[Amazon EC2|EC2 instances]] will get at least a private internal IPv4 and a public IPv6.

If we cannot launch an EC2 instance in our subnet. It’s not because it cannot acquire an IPv6, it’s because there are no available IPv4 in our subnet. To solve that we should create a new IPv4 [[CIDR and IP Addressing|CIDR]] in our subnet.

---
**Up:** [[Amazon VPC]] · **Map:** [[Networking and Content Delivery Map]]
