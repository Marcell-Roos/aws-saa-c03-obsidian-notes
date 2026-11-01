---
tags: [service, cat/networking, scope/in]
aliases: ["Global Accelerator"]
---

# AWS Global Accelerator

**AWS Global Accelerator** - improves global application availability and performance using the AWS global network. It leverages the AWS internal network to optimize the route to our application (AWS quotes up to 60%).

It provides two static IP addresses that serve as a fixed entry point to our application. These IP addresses are anycast from AWS edge locations, ensuring user traffic is directed to the closest AWS region.

It works with Elastic IP, [[Amazon EC2|EC2 instances]], [[Application Load Balancer|ALB]], [[Network Load Balancer|NLB]]. We can use [[AWS Shield]] for DDoS protection.

Global Accelerator performs a health check of our applications. It helps make our application global (failover less than 1 minute for unhealthy) and it’s great for [[Disaster Recovery Strategies|disaster recovery]].

See [[CloudFront vs Global Accelerator]].

## Exam tasks
- [[Task 3.4 Determine high-performing and or or scalable network architectures]]
- [[Task 4.4 Design cost-optimized network architectures]]

---
**Map:** [[Networking and Content Delivery Map]]
