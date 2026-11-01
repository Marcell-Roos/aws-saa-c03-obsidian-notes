---
tags: [service, cat/serverless, scope/in]
---

# Lambda in a VPC

By default, our [[AWS Lambda|Lambda function]] is launched outside our own [[Amazon VPC|VPC]]. Therefore, it cannot access resources in our VPC ([[Amazon RDS|RDS]], [[Amazon ElastiCache|ElastiCache]], etc).

We must define the VPC ID, the subnets and [[Security Groups|security groups]]. Lambda will create an [[Elastic Network Interface|ENI]] in our subnets.

If Lambda functions directly access our database, they may open too many connections under high load. We can use [[RDS Proxy]] to improve scalability. The Lambda function must be deployed in our VPC, because RDS Proxy is never publicly accessible.

---
**Up:** [[AWS Lambda]] · **Map:** [[Serverless Map]]
