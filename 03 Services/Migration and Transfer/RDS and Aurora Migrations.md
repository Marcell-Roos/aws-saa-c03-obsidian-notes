---
tags: [service, cat/migration, scope/in]
---

# RDS and Aurora Migrations

**[[Amazon RDS|RDS]] MySQL → [[Amazon Aurora|Aurora]] MySQL**

- **Option 1**: DB Snapshots from RDS MySQL restored as MySQL Aurora DB.
- **Option 2**: Create an Aurora [[RDS Read Replicas|Read Replica]] from our RDS MySQL and when the replication lag is 0, promote it as its own DB cluster (can take time and money).

**External MySQL → Aurora MySQL**

- **Option 1**: Use Percona XtraBackup to create a file backup in [[Amazon S3|S3]] and then create an Aurora MySQL DB from S3.
- **Option 2**: Create an Aurora MySQL DB and use mysqldump utility to migrate MySQL into Aurora (slower than option 1).

**RDS Postgres → Aurora Postgres**

- **Option 1**: DB Snapshots from RDS Postgres restored as Postgres Aurora DB.
- **Option 2**: Create an Aurora Read Replica from our RDS Postgres and when the replication lag is 0, promote it as its own DB cluster (can take time and money).

**External Postgres → Aurora Postgres**

- Create backup and put it in S3 then import it using the aws_s3 Aurora extension.

**If both databases are up and running, use [[AWS DMS|DMS]].**

## Exam tasks
- [[Task 4.3 Design cost-optimized database solutions]]

---
**Up:** [[AWS DMS]] · **Map:** [[Migration and Transfer Map]]
