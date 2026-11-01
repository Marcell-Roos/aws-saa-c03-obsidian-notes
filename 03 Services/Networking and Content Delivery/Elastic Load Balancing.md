---
tags: [service, cat/networking, scope/in]
aliases: ["ELB", "load balancer", "load balancers", "Load balancers"]
---

# Elastic Load Balancing

**Load balancers** are servers that forward internet traffic to multiple servers ([[Amazon EC2|EC2 Instances]]) downstream.

Pros of using a load balancer:

- **High availability across zones.**
- Spread load across multiple downstream instances.
- Expose a single point of access ([[DNS Fundamentals|DNS]]) to our application.
- Handle failures of downstream instances.
- **Do regular health checks to our instances**.
- Provide SSL termination for our websites easily.

**ELB** is a managed load balancer. AWS guarantees that will be working, takes care of upgrades, maintenance and [[Scalability and High Availability|high availability]]. ELB captures the logs and stores them in the [[Amazon S3|S3 bucket]] that we specify as compressed files. We can disable access logging at any time.

Health checks are crucial for Load Balancers. They enable the load balancer to know if instances it forwards traffic to are available to reply to requests. The health check is done on a port and a route (/health is common).

There are 3 types of load balancers offered by AWS:

- **[[Application Load Balancer]] (ALB)** (HTTP/HTTPS only) - Layer 7
- **[[Network Load Balancer]] (NLB)** (High performance, allows for TCP/UDP) - Layer 4
- **[[Gateway Load Balancer]] (GWLB)** - Layer 3

Some load balancers can be setup as internal (private) or external (public) ELBs.

**ELB [[Security Groups]]**

The load balancer's security group allows HTTP and HTTPS from anywhere. The instances' security group allows traffic **only from the load balancer's security group**.

## In this topic
- [[Application Load Balancer]]
- [[ELB Cross-Zone Load Balancing]]
- [[ELB Deregistration Delay]]
- [[ELB SSL Certificates and SNI]]
- [[ELB Sticky Sessions]]
- [[Gateway Load Balancer]]
- [[Network Load Balancer]]

## Exam tasks
- [[Task 2.1 Design scalable and loosely coupled architectures]]
- [[Task 4.4 Design cost-optimized network architectures]]

---
**Map:** [[Networking and Content Delivery Map]]
