---
tags: [exam, scope/in]
---

# Exam Traps

Wrong answers that sound right. Adapted from RonitSachdev's guide (CC BY 4.0), with updates marked. See [[Licences and Attribution]].

| Trap | Truth |
| --- | --- |
| Read from the [[RDS Multi-AZ]] standby | A Multi-AZ **instance** standby isn't readable, so use [[RDS Read Replicas\|read replicas]]. A Multi-AZ **DB cluster** does have two readable standbys |
| CNAME at the zone apex | Not allowed. Use an [[CNAME vs Alias Records\|Alias record]] |
| Add a deny rule to a [[Security Groups\|security group]] | Security groups only allow. Deny lives in [[Network ACLs\|NACLs]] |
| Private [[Amazon VPC\|subnet]] reaches [[Amazon S3\|S3]] through NAT | Works but costs money. A [[VPC Endpoints\|Gateway Endpoint]] is free and private |
| Run a 20-minute job in [[AWS Lambda\|Lambda]] | Lambda stops at 15 minutes. Use [[AWS Fargate\|Fargate]], Batch or [[AWS Step Functions\|Step Functions]] |
| Mount [[Amazon EFS\|EFS]] on Windows | EFS is Linux only. Use [[FSx for Windows File Server]] |
| [[AWS Snow Family\|Snowball]] imports directly into Glacier | It lands in S3, then a lifecycle rule moves it |
| A-B and B-C peering lets A reach C | Peering isn't transitive. Use Transit Gateway or a direct peering |
| Encrypt an existing RDS or EBS volume in place | Impossible. Snapshot, copy with encryption, restore |
| FIPS Level 3 means CloudHSM | **Updated:** KMS HSMs are now FIPS 140-3 Level 3 too. The real difference is that CloudHSM is single-tenant and you control the keys. Older questions may still expect CloudHSM |
| Shield Standard stops layer 7 attacks | Standard covers layers 3 and 4. Layer 7 needs WAF or Shield Advanced |
| Apply an SCP to the management account | SCPs never affect the management account |
| Replay DynamoDB Streams from last month | Streams keep 24 hours. Use Kinesis Data Streams for longer retention |
| Give an ALB a static IP | ALBs have none. Use an NLB, or Global Accelerator |
| Add an LSI to an existing table | LSIs are set at table creation. Add a GSI instead |
| Accelerate UDP with CloudFront | CloudFront is for HTTP(S). Use Global Accelerator |
| Parameter Store rotates passwords | No native rotation. Use Secrets Manager |
| One NAT Gateway serves all AZs | A zonal gateway dies with its AZ. Use one per AZ, or **updated:** a regional NAT Gateway |
| SNS alone keeps messages for offline consumers | SNS doesn't persist them. Use SNS to SQS |
| Direct Connect is encrypted | It's private, not encrypted. Add a VPN over it or MACsec |

---
**Up:** [[SAA-C03 Exam Overview]]
