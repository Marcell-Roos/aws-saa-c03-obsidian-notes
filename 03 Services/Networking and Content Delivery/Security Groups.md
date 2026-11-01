---
tags: [service, cat/networking, scope/in]
aliases: ["security group", "security groups", "Security Group"]
---

# Security Groups

**Security Groups** are the fundamental of network security in AWS. They control how traffic is allowed INTO or OUT of our [[Amazon EC2|EC2 Instances]].

Security groups only contain allow rules. Rules can reference by IP or by another security group.

Security groups are acting as a “firewall” on EC2 instances. They regulate access to ports, authorised IP ranges, control of inbound network and control of outbound network.

Security groups can be attached to multiple instances. They are locked down to a region/VPC combination.

It’s good practice to maintain one separate security group for SSH access.

If application is not accessible (time out), then it is a security group issue and if application gives a “connection refused”, then it is an application error.

**Security Groups** - firewall that controls traffic to and from an EC2 instance. It can have only ALLOW rules. Rules include IP addresses and other security groups.

## Exam tasks
- [[Task 1.2 Design secure workloads and applications]]

---
**Up:** [[Amazon VPC]] · **Map:** [[Networking and Content Delivery Map]]
