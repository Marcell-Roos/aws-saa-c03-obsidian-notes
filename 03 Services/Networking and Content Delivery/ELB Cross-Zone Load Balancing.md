---
tags: [service, cat/networking, scope/in]
aliases: ["Cross-Zone Load Balancing"]
---

# ELB Cross-Zone Load Balancing

**Cross-Zone Load Balancing** is a feature [[Elastic Load Balancing|ELB]] that helps distribute incoming traffic more evenly across the registered instances in different AZs.

- **[[Application Load Balancer|ALB]]**: Cross-Zone Load Balancing is always enabled at the load balancer level and can be turned off at the target group level. We don't pay for inter AZ data.
- **[[Network Load Balancer|NLB]]** and **[[Gateway Load Balancer|GWLB]]**: It is disabled by default and can be enabled via the [[AWS Management Console]], CLI, or API. We need to pay charges for inter AZ data if enabled.

---
**Up:** [[Elastic Load Balancing]] · **Map:** [[Networking and Content Delivery Map]]
