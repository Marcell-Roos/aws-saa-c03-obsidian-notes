---
tags: [service, cat/networking, scope/in]
aliases: ["Bastion Host", "bastion hosts"]
---

# Bastion Hosts

**Bastion Host** is a special-purpose instance designed to provide secure access to our private network in the AWS cloud. It acts as a bridge or "**jump box**" for administrative tasks, allowing us to securely manage and administer our instances in private [[Amazon VPC|subnets]].

Bastion Host [[Security Groups|security group]] must allow inbound from the internet on port 22 from restricted [[CIDR and IP Addressing|CIDR]], for example the public CIDR of our corporation.

Security Group of the [[Amazon EC2|EC2 instances]] must allow the Security Group of the Bastion Host, or the private IP of the Bastion Host.

## Exam tasks
- [[Task 1.2 Design secure workloads and applications]]

---
**Up:** [[Amazon VPC]] · **Map:** [[Networking and Content Delivery Map]]
