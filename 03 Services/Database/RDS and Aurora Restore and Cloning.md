---
tags: [service, cat/database, scope/in]
aliases: ["Aurora Database Cloning"]
---

# RDS and Aurora Restore and Cloning

**[[Amazon RDS|RDS]] & [[Amazon Aurora|Aurora]] Restore Options**

- **Restoring RDS/Aurora backup or snapshot** - creates a new database.
- **Restoring MySQL RDS database from [[Amazon S3|S3]]**
    1. Create a backup of our on-premises database.
    2. Store it on S3.
    3. Restore the backup file onto a new RDS instance running MySQL.
- **Restoring MySQL Aurora cluster from S3**
    1. Create a backup of our on-premises database using Percona XtraBackup.
    2. Store the backup file on S3.
    3. Restore the backup file onto a new Aurora cluster running MySQL.

**Aurora Database Cloning**

It is possible to create a new Aurora DB Cluster from an existing one. It is cost effective and faster than snapshot & restore.

It uses copy-on-write protocol - initially, the new database cluster uses the same data volume as the original database cluster (no copying needed). When updates are made to the new database cluster data, then additional storage is allocated and data is copied to be separated.

Cloning is useful to create a “staging” database from a “production” database without impacting the production database.

---
**Up:** [[Amazon RDS]] · **Map:** [[Database Map]]
