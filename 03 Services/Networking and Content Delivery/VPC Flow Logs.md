---
tags: [service, cat/networking, scope/in]
aliases: ["Flow Logs"]
---

# VPC Flow Logs

**VPC Flow Logs** capture information about IP traffic going into our interfaces. There are also Subnet Flow Logs and [[Elastic Network Interface|ENI]] Flow Logs. [[Amazon VPC|VPC]] Flow logs data can go to [[Amazon S3|S3]], [[CloudWatch Logs]] and [[Amazon Data Firehose]].

srcaddr & dstaddr - identify problematic IP.

srcport & dstport - identify problematic ports.

action - success or failure of the request due to [[Security Groups|Security Group]]/NACL.

We can query VPC Flow Logs using [[Amazon Athena|Athena]] on S3 or CloudWatch Logs Insights.

**Troubleshooting SG & [[Network ACLs|NACL]]**

We can look at the “ACTION” field to troubleshoot problems.

- Inbound REJECT ⇒ NACL or SG problem.
- Inbound ACCEPT, Outbound REJECT ⇒ NACL problem.
- Outbound REJECT ⇒ NACL or SG problem.
- Outbound ACCEPT, Inbound REJECT ⇒ NACL problem.
- **VPC Flow Logs Architectures.** Send logs to CloudWatch Logs with a metric filter and alarm, or to S3 and query them with Athena and show results in [[Amazon Quick]].

---
**Up:** [[Amazon VPC]] · **Map:** [[Networking and Content Delivery Map]]
