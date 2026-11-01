---
tags: [service, cat/database, scope/in]
---

# RDS and Aurora Security

- **At-rest encryption** - database master & replicas encryption using [[AWS KMS|KMS]] (must be defined as launch time). If the master is not encrypted, the [[RDS Read Replicas|read replicas]] cannot be encrypted. To encrypt an un-encrypted database we should go through a database snapshot & restore as encrypted.
- **In-flight encryption** - they are TLS-ready by default and use the TLS root certificates client-side.
- **[[AWS IAM|IAM]] Authentication** - we should use IAM roles to connect to our database. Instead of username and password, we use an authentication token. IAM database authentication works with MariaDB, MySQL and PostgreSQL. Network traffic to and from the database is encrypted using SSL.
- **[[Security Groups]]** - control network access to our databases.
- **No SSH available** (except on [[RDS Custom]]).
- **Audit Logs** - can be enabled and sent to [[CloudWatch Logs]] for longer retention.

To encrypt an existing unencrypted database, snapshot it, copy the snapshot with encryption, and restore.

## Exam tasks
- [[Task 1.3 Determine appropriate data security controls]]

---
**Up:** [[Amazon RDS]] · **Map:** [[Database Map]]
