---
tags: [service, cat/database, scope/in]
aliases: ["PITR"]
---

# DynamoDB Backups and S3 Integration

**[[Amazon DynamoDB|DynamoDB]] Backups**

- **Continuous backups using PITR** - optionally enabled for the last 35 days. PITR to any time within the backup window. The recovery process creates a new table.
- **On-demand backups** - full backups for long-term retention, until explicitly deleted. It doesn't affect performance or latency. Can be configured and managed in [[AWS Backup]]. The recovery process creates a new table.

**DynamoDB Integration with [[Amazon S3|S3]]**

- **Export to S3** (**must enable PITR**) - works for any point of time in the last 35 days. It doesn't affect the read capacity of our table. We can perform data analysis on top of DynamoDB and ETL on top of S3 data before importing back to DynamoDB.
- **Import from S3** - import CSV, DynamoDB JSON or ION format. It doesn't consume any write capacity. It creates a new table. Import errors are logged in [[CloudWatch Logs]].

---
**Up:** [[Amazon DynamoDB]] · **Map:** [[Database Map]]
