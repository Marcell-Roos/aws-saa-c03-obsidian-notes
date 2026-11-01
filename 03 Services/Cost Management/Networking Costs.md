---
tags: [service, cat/cost, scope/in]
---

# Networking Costs

Egress traffic - outbound traffic (AWS → Outside). [[AWS Direct Connect|DX]] locations that are co-located in the same AWS Region result in lower cost for egress network.

Ingress traffic - inbound traffic (Outside → AWS), typically free.

We should try to keep as much internet traffic within AWS to minimize costs.

**[[NAT Gateways|NAT Gateway]] vs [[VPC Endpoints|VPC Endpoint]] Pricing**

Reaching [[Amazon S3|S3]] through a NAT Gateway incurs hourly and per-GB charges. A Gateway Endpoint in the same Region is free.

Rules of thumb, as the source's tables were images:

- Data into AWS is generally free.
- Data out to the internet costs the most.
- Traffic between AZs is charged, and traffic in one AZ over private IPs is generally free.
- Use private IPs, not public, between instances.
- S3 Gateway Endpoints avoid NAT Gateway processing charges.
- [[Amazon CloudFront|CloudFront]] can reduce data-out costs.

## Exam tasks
- [[Task 4.4 Design cost-optimized network architectures]]

---
**Up:** [[Amazon VPC]] · **Map:** [[Cost Management Map]]
