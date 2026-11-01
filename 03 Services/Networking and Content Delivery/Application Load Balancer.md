---
tags: [service, cat/networking, scope/in]
aliases: ["ALB", "ALBs"]
---

# Application Load Balancer

**ALB** operates at the application layer (Layer 7) of the OSI model, which enables it to make routing decisions based on content. It supports redirects (for example from HTTP to HTTPS).

ALB supports target groups, which are logical groups of resources. Each target group can have different health checks and configurations, allowing for fine-grained control. ALB can route to multiple target groups and health checks are at the target group level.

Slow Start Mode - allows us to add new targets without overwhelming them with a flood of requests.

**Target Groups**:

- **[[Amazon EC2|EC2 Instances]]** (can be managed by an [[Amazon EC2 Auto Scaling|ASG]]).
- **[[Amazon ECS|ECS tasks]]** (managed by ECS).
- **[[AWS Lambda|Lambda functions]]**.
- **IP Addresses** (must be private IPs).

ALBs are a great fit for microservices & container-based applications. They have a port mapping feature to redirect to a dynamic port in ECS.

**Routing Features**

- **Path-based Routing** - based on the URL path (example.com/users).
- **Host-based Routing** - based on the Host field in the HTTP header (one.example.com).
- **Query String and Header-based Routing** - ased on the query string or specific headers in the HTTP request (example.com/users?id=123&order=false).

The application servers don’t see the IP of the client directly. The true IP of the client is inserted in the header **X-Forwarded-For**.

## Exam tasks
- [[Task 2.1 Design scalable and loosely coupled architectures]]

---
**Up:** [[Elastic Load Balancing]] · **Map:** [[Networking and Content Delivery Map]]
