---
tags: [reference, scope/in]
---

# Limits and Numbers

All values were checked in AWS docs on 1 November 2026. Default quotas can change, and many are adjustable.

| Service | Limit | Value |
| --- | --- | --- |
| [[Amazon S3]] | Max object | 48.8 TiB |
| [[Amazon S3\|S3]] | Single PUT | 5 GiB |
| S3 | Multipart parts | 10,000 |
| S3 | Requests per prefix | 3,500 writes, 5,500 reads per second |
| [[EBS Volume Types]] | [[EBS Volume Types\|gp3]] | 1 GiB to 64 TiB, 3,000 to 80,000 IOPS, 125 to 2,000 MiB/s |
| [[Amazon EBS\|EBS]] | io2 Block Express | Up to 64 TiB, 256,000 IOPS |
| EBS | st1 | Max 500 MiB/s |
| [[EBS Multi-Attach]] | Instances | 16 Nitro instances in one AZ |
| [[AWS Lambda]] | Memory | 128 MB to 10,240 MB |
| [[AWS Lambda\|Lambda]] | Timeout | 15 minutes |
| Lambda | /tmp | 512 MB to 10,240 MB |
| Lambda | Package | 50 MB zipped, 250 MB unzipped, 10 GB container |
| Lambda | Payload | 6 MB sync, 1 MB async, 200 MB streamed |
| Lambda | Concurrency | 1,000 default, +1,000 environments per 10 seconds |
| Lambda | Environment variables | 4 KB |
| Lambda | Layers | 5 |
| [[Amazon SQS]] | Message size | 1 MiB |
| [[Amazon SQS\|SQS]] | Retention | 1 minute to 14 days, default 4 days |
| SQS | Visibility timeout | Default 30 seconds, max 12 hours |
| SQS | Delay | Up to 15 minutes |
| SQS | Long polling | Up to 20 seconds |
| [[SQS FIFO Queues]] | Throughput | 300 TPS, 3,000 batched, 70,000 in high-throughput mode |
| [[Amazon SNS]] | Message size | 256 KiB default, up to 1 MiB |
| [[Kinesis Data Streams]] | Record | Up to 10 MiB |
| [[Kinesis Data Streams\|KDS]] | Retention | 24 hours to 365 days |
| KDS | Read per shard | 2 MB/s |
| [[Amazon DynamoDB]] | Item | 400 KB |
| [[Amazon DynamoDB\|DynamoDB]] | [[DynamoDB Backups and S3 Integration\|PITR]] | 1 to 35 days |
| [[DynamoDB Streams]] | Retention | 24 hours |
| [[Amazon RDS]] | Read replicas | 15 |
| [[Amazon RDS\|RDS]] | Backup retention | 0 to 35 days |
| [[Amazon Aurora]] | Volume | 256 TiB on recent versions |
| [[Amazon Aurora\|Aurora]] | Replicas | 15 |
| [[Aurora Global Database]] | Secondary Regions | 10, with 16 readers each |
| [[Amazon VPC]] | [[CIDR and IP Addressing\|CIDR]] size | /28 to /16 |
| [[Amazon VPC\|VPC]] | Reserved IPs | 5 per subnet |
| VPC | IPv4 CIDRs | 5 default, up to 50 |
| VPC | VPCs per Region | 5 default |
| [[Network ACLs]] | Rules | 20 default |
| [[AWS Site-to-Site VPN]] | Tunnel | 1.25 Gbps, 5 Gbps large bandwidth |
| [[AWS Direct Connect]] | Dedicated | 1, 10, 100, 400 Gbps |
| [[AWS Direct Connect\|Direct Connect]] | Hosted | 50 Mbps to 25 Gbps |
| [[Amazon API Gateway]] | Timeout | 29 seconds default |
| [[Amazon API Gateway\|API Gateway]] | Payload | 10 MB |
| API Gateway | Account throttle | 10,000 requests per second |
| [[EC2 Placement Groups]] | Spread | 7 running instances per AZ |
| Placement groups | Partition | 7 partitions per AZ |
| [[EC2 Hibernate]] | RAM | Under 150 GiB on Linux |
| [[EC2 Spot Instances]] | Notice | 2 minutes |
| [[AWS Step Functions]] | Standard, Express | 1 year, 5 minutes |
| [[AWS CloudTrail]] | Event history | 90 days |

---
**Up:** [[Home]]
