---
tags: [service, cat/compute, scope/in]
aliases: ["ENI", "ENIs", "elastic network interface"]
---

# Elastic Network Interface

**ENI** is a logical networking component in a [[Amazon VPC|VPC]] that represents a virtual network card.

ENI Attributes:

- **Primary Private IP Address**
- **Secondary Private IP Addresses**
- **One Elastic IP Addresses**
- **One Public IPv4 Address**
- **MAC Address**
- **[[Security Groups]]**

ENIs can be attached to instances in the same VPC, but must reside in the same AZ. We can attach a secondary ENI to an instance and use it for **failover** scenarios. If the primary instance fails, we can attach the ENI to a standby instance.

Every instance gets a primary ENI (eth0) at launch, and that one can't be detached; it dies with the instance. Additional secondary ENIs can be attached, up to a limit that depends on the instance type (roughly 2 on the smallest types, 15+ on large ones).

---
**Up:** [[Amazon EC2]] · **Map:** [[Compute Map]]
