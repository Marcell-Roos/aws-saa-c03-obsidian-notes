---
tags: [drill, scope/in]
---

# Drill Well Architected

Adapted from [RonitSachdev/aws-saa-c03-guides](https://github.com/RonitSachdev/aws-saa-c03-guides) (CC BY 4.0), with outdated facts changed.

## Question patterns

- *"Two solutions both meet requirements; question asks for the MOST cost-effective"* → **the cheaper one that still works** (Cost Optimization is steering — e.g., Spot over On-Demand for fault-tolerant batch)
- *"Improve reliability of a single-AZ database"* → **Enable Multi-AZ** (Reliability pillar: survive AZ failure with automatic failover)
- *"LEAST operational overhead to run containers"* → **[[AWS Fargate|Fargate]] over [[Amazon EC2|EC2]] launch type** (Operational Excellence/managed-first: no servers to patch)
- *"Improve performance for global users"* → **[[Amazon CloudFront|CloudFront]]** (Performance Efficiency: go global, cache at the edge)
- *"Ensure the architecture follows AWS best practices at no additional cost"* → **[[AWS Well-Architected Tool]]** (free console questionnaire → improvement plan)
- *"Reduce the environmental impact of the workload"* → **Graviton instances / serverless** (Sustainability: maximize utilization)

## Pocket card

| Keyword | Answer |
|---|---|
| IaC, small reversible changes | Operational Excellence ([[AWS CloudFormation\|CloudFormation]]) |
| Least privilege, encrypt everywhere | Security ([[AWS IAM\|IAM]], [[AWS KMS\|KMS]], [[Amazon GuardDuty\|GuardDuty]]) |
| Survive failure, stop guessing capacity | Reliability (Multi-AZ, [[Amazon EC2 Auto Scaling\|ASG]], [[Amazon Route 53\|Route 53]]) |
| Right tool, serverless-first, edge | Performance Efficiency ([[AWS Lambda\|Lambda]], CloudFront) |
| Pay for what you use, measure spend | Cost Optimization ([[AWS Cost Explorer\|Cost Explorer]], [[Savings Plans]], Spot) |
| Maximize utilization, Graviton | Sustainability |
| Free best-practices review | Well-Architected Tool |
| "MOST cost-effective / LEAST overhead" | The qualifier picks between two working answers |

---
**Up:** [[Drills Map]]
