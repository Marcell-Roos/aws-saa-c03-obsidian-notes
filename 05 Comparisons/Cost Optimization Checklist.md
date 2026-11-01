---
tags: [comparison, scope/in]
---

# Cost Optimization Checklist

**Compute**
- Rightsize with [[AWS Compute Optimizer]].
- Use [[Savings Plans]] for steady use and [[EC2 Spot Instances]] for interruptible use.
- Stop idle dev environments, or use [[EC2 Hibernate]].

**Storage**
- Use [[S3 Lifecycle Rules]] or [[S3 Storage Classes|Intelligent-Tiering]].
- Prefer [[EBS Volume Types|gp3]] over gp2.
- Delete unattached [[Amazon EBS|EBS volumes]] and old snapshots.

**Database**
- Use [[Aurora Serverless]] or [[Amazon DynamoDB|DynamoDB]] on-demand for spiky load.
- Cache reads with [[Amazon ElastiCache]].
- Use [[Amazon Aurora|Aurora]] I/O-Optimized when I/O is at least 25% of Aurora spend.

**Network**
- Use [[VPC Endpoints|Gateway Endpoints]] for [[Amazon S3|S3]] and DynamoDB.
- Keep traffic in one AZ where availability allows.
- Use [[Amazon CloudFront]] to reduce origin data transfer.
- See [[Networking Costs]].

**Visibility**
- [[AWS Cost Explorer]], [[AWS Budgets]], [[Cost Allocation Tags]], [[AWS Cost Anomaly Detection]]

## Exam tasks
- [[Task 4.1 Design cost-optimized storage solutions]]
- [[Task 4.2 Design cost-optimized compute solutions]]
- [[Task 4.4 Design cost-optimized network architectures]]

---
**Up:** [[Decision Guides Map]]
