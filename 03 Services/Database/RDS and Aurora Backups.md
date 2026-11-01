---
tags: [service, cat/database, scope/in]
---

# RDS and Aurora Backups

**[[Amazon RDS|RDS]] Backups**

- **Automated backups**
    - Daily full backup of database (during the backup window).
    - Transaction logs are backed-up by RDS every 5mins.

    With automated backups we have ability to restore to any point in time (from oldest backup to 5mins ago).

    Retention of backups can be set from 1 to 35 days (set to 0 to disable automated backups.)

- **Manual DB Snapshots**

    They are manually triggered by the user. Retention of backups can be set for as long as needed.

    > In a stopped RDS database, we will still pay for storage. **If we plan on stopping it for a long time, we should use snapshot & restore instead.**

**[[Amazon Aurora|Aurora]] Backups**

- **Automated backups** - from 1 to 35 days (cannot be disabled). We have point-in-time recovery in that timeframe.
- **Manual DB Snapshots** - manually triggered by the user. Retention of backups can be set for as long as needed.

## Exam tasks
- [[Task 4.3 Design cost-optimized database solutions]]

---
**Up:** [[Amazon RDS]] · **Map:** [[Database Map]]
