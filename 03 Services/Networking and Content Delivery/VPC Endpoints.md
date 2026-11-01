---
tags: [service, cat/networking, scope/in]
aliases: ["VPC Endpoint", "Gateway Endpoints", "Interface Endpoints", "Gateway Endpoint"]
---

# VPC Endpoints

**VPC Endpoints** (powered by [[AWS PrivateLink]]) allow us to connect to AWS Services using a private network instead of the public internet. It gives us enhanced security and lower latency to access AWS services.

- **Interface Endpoints** (powered by PrivateLink) - provisions an [[Elastic Network Interface|ENI]] (private IP address) as an entry point (must attach a [[Security Groups|Security Group]]). It supports most AWS services. We pay per hour and per GB of data processed.
- **Gateway Endpoints** - provisions a gateway and must be used as a target in a [[Internet Gateway and Route Tables|route table]] (does not use security groups). It supports [[Amazon S3|S3]] and [[Amazon DynamoDB|DynamoDB]] and it is free.

    We can attach an endpoint policy that controls access to the service to which we are connecting. We can modify the endpoint policy attached to our endpoint and add or remove the route tables used by the endpoint. An endpoint policy does not override or replace [[AWS IAM|IAM]] user policies or service-specific policies.

| | Gateway | Interface |
| --- | --- | --- |
| Services | S3, DynamoDB | Most AWS services, and S3 |
| How | Route table target | ENI with a private IP |
| Cost | Free | Hourly + per GB |
| Security | Endpoint policy | Security group + endpoint policy |
| On-premises access | No | Yes, over VPN or [[AWS Direct Connect\|Direct Connect]] |

## Exam tasks
- [[Task 1.2 Design secure workloads and applications]]
- [[Task 4.4 Design cost-optimized network architectures]]

---
**Up:** [[Amazon VPC]] · **Map:** [[Networking and Content Delivery Map]]
