---
tags: [drill, scope/in]
---

# Drill RDS Aurora

Adapted from [RonitSachdev/aws-saa-c03-guides](https://github.com/RonitSachdev/aws-saa-c03-guides) (CC BY 4.0), with outdated facts changed.

## Question patterns

- *"Database must survive an AZ failure with no manual intervention"* → **Multi-AZ** ("survive failure" + "automatic" = spare tire, 60–120s [[DNS Fundamentals|DNS]] flip).
- *"Reporting/analytics queries are slowing down the production database"* → **[[RDS Read Replicas|Read Replica]]** (offload reads to a checkout lane — but if the queries are the *same ones repeatedly*, **[[Amazon ElastiCache|ElastiCache]]** wins; replica is for **diverse/complex** queries).
- *"[[AWS Lambda|Lambda functions]] are exhausting database connections"* → **[[RDS Proxy]]** (Lambda + [[Amazon RDS|RDS]] = Proxy, every time).
- *"Encrypt an existing unencrypted RDS database"* → **snapshot → copy with encryption → restore** (encryption is creation-time only; this is the snapshot dance).
- *"Global application needs cross-region DR with less than 1 minute recovery"* → **[[Aurora Global Database]]** ([[RPO and RTO|RPO]] ~1s, RTO <1min — nothing else touches it).
- *"Dev database sits idle nights and weekends; minimize cost"* → **[[Aurora Serverless]] v2** (spiky/idle/unpredictable = serverless).
- *"Need a full copy of the production database for testing, quickly and cheaply"* → **[[Amazon Aurora|Aurora]] Cloning** (copy-on-write = instant, near-free until it diverges).
- *"Developer ran a bad DELETE; restore the database to 5 minutes ago as fast as possible"* → **Aurora Backtrack** (rewind in place — no restore, no new instance).
- *"Compliance requires database backups kept for 7 years"* → **Manual snapshots** (automated backups cap at 35 days).
- *"Application needs OS-level access / a custom database engine"* → **[[Amazon EC2|EC2]]** (or [[RDS Custom]] for Oracle/SQL Server) — plain RDS gives no OS access.

## Pocket card

| Keyword in question | Answer |
|---|---|
| survive AZ failure, auto-failover | **Multi-AZ** (sync, 60–120s, DNS flip) |
| standby serves reads | **TRAP — never** |
| scale reads, offload reporting | **Read Replica** (async, up to 15, manual promotion) |
| replica auto-failover | **TRAP — promotion is manual** |
| same queries over and over | ElastiCache (not a replica) |
| Lambda + RDS connections | **RDS Proxy** |
| backups > 35 days / "retain X years" | **Manual snapshot** |
| restore to any point in time (≤35 days) | Automated backups / [[DynamoDB Backups and S3 Integration\|PITR]] |
| encrypt existing DB | **Snapshot → copy-encrypted → restore** |
| OS access / custom engine | EC2 or RDS Custom |
| failover <30s, 15 low-lag replicas, 256 TiB autogrow on recent versions | **Aurora** |
| spiky / idle / unpredictable load | **Aurora Serverless v2** |
| cross-region DR, RPO ~1s, RTO <1min | **Aurora Global Database** |
| instant prod copy for staging | **Aurora Cloning** |
| undo mistake fast, no restore | **Aurora Backtrack** |

---
**Up:** [[Drills Map]]
