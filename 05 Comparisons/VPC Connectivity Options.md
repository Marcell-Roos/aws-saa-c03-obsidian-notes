---
tags: [comparison, scope/in]
---

# VPC Connectivity Options

Adapted from devesh-talreja's cheat sheet (MIT).

| Option | What it is | Use when |
| --- | --- | --- |
| [[AWS Site-to-Site VPN]] | IPsec over the internet | Quick and cheap, variable latency. 1.25 Gbps per tunnel, or 5 Gbps with Large Bandwidth Tunnels |
| [[AWS Direct Connect]] | Private dedicated line | Consistent, high bandwidth |
| [[VPC Peering]] | Direct VPC-to-VPC link | A few [[Amazon VPC\|VPCs]], no transitive routing |
| [[AWS Transit Gateway]] | Central hub | Many VPCs and on-premises networks |
| [[AWS PrivateLink]] | Private access to one service | SaaS or one-way exposure |
| [[VPC Endpoints]] | Private route to AWS services | [[Amazon S3\|S3]] and [[Amazon DynamoDB\|DynamoDB]] (Gateway) or others (Interface) |
| [[AWS Client VPN]] | Per-user VPN | Remote workers |

## Exam tasks
- [[Task 3.4 Determine high-performing and or or scalable network architectures]]

---
**Up:** [[Comparisons Map]]
