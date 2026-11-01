---
tags: [service, cat/networking, scope/in]
aliases: ["NAT Instance"]
---

# NAT Instances

**NAT Instance** allows [[Amazon EC2|EC2 instance]] in private [[Amazon VPC|subnets]] to connect to the internet. They must be launched in a public subnet and we must disable EC2 source/destination check setting and have Elastic IP attached to it.

[[Internet Gateway and Route Tables|Route Tables]] must be configured to route traffic from private subnets to the NAT Instance.

There is a pre-configured Amazon Linux [[Amazon Machine Image|AMI]] for NAT Instance. NAT instances are not highly available, we need to create an [[Amazon EC2 Auto Scaling|ASG]] in multi-AZ and internet traffic bandwidth depends on EC2 instance type.

---
**Up:** [[Amazon VPC]] · **Map:** [[Networking and Content Delivery Map]]
