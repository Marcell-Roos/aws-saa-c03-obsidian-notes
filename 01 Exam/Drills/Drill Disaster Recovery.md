---
tags: [drill, scope/in]
---

# Drill Disaster Recovery

Adapted from [RonitSachdev/aws-saa-c03-guides](https://github.com/RonitSachdev/aws-saa-c03-guides) (CC BY 4.0), with outdated facts changed.

## Question patterns

- *"[[RPO and RTO|RTO]] of 10 minutes, RPO of seconds, keep costs reasonable"* → **[[Disaster Recovery Strategies|Warm Standby]]** (Active-Active also works but costs more; Pilot Light is too slow)
- *"DR needed at the LOWEST cost; hours of downtime acceptable"* → **Backup & Restore** (cheapest strategy that meets a relaxed RTO)
- *"Application must survive a region failure with zero downtime and zero data loss"* → **Multi-Site Active-Active** (only ~zero RPO/RTO option)
- *"Database continuously replicated to DR region; [[Amazon EC2|EC2]] launched only during a disaster"* → **Pilot Light** (core data live, compute off)
- *"Centrally manage and automate backups of [[Amazon EBS|EBS]], [[Amazon RDS|RDS]], and [[Amazon DynamoDB|DynamoDB]] across the organization"* → **[[AWS Backup]]** (one service, backup plans + vault lock)
- *"Cost-effective DR for 200 on-premises servers into AWS"* → **[[AWS Elastic Disaster Recovery|Elastic Disaster Recovery]] (DRS)** (continuous block replication, pay tiny until failover)
- *"Global relational database with cross-region RPO of ~1 second"* → **[[Aurora Global Database]]** (RPO 1s, RTO under a minute)
- *"Automatically route users to the standby region when the primary fails"* → **[[Amazon Route 53|Route 53]] failover routing with health checks**

## Pocket card

| Keyword | Answer |
|---|---|
| Max data loss | RPO |
| Max downtime | RTO |
| Cheapest, RTO hours | Backup & Restore |
| DB replicated, servers off | Pilot Light |
| Scaled-down copy running | Warm Standby |
| Zero RPO/RTO, both live | Multi-Site Active-Active |
| RPO 1s / RTO <1 min relational | Aurora Global Database |
| Multi-region multi-active NoSQL | [[DynamoDB Global Tables]] |
| Centralized cross-service backups | AWS Backup (+ [[S3 Object Lock and Glacier Vault Lock\|Vault Lock]]) |
| Replicate on-prem servers for DR | Elastic Disaster Recovery (DRS) |
| [[DNS Fundamentals\|DNS]] failover to DR region | Route 53 failover routing |

---
**Up:** [[Drills Map]]
