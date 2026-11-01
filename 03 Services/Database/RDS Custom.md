---
tags: [service, cat/database, scope/in]
---

# RDS Custom

> [!warning] Oracle sunset
> RDS Custom for Oracle reaches end of support on 31 March 2027.

**RDS Custom** is a feature that provides a way to use a custom database engine. It’s used for Oracle and Microsoft SQL Server with OS and database customization (**access to the underlying database and OS**).

We can configure settings, install patches, access underlying [[Amazon EC2|EC2]] using SSH or [[AWS Systems Manager|SSM]].

To perform our customization it is recommended deactivate Automation Mode (better to take a DB snapshot before).

---
**Up:** [[Amazon RDS]] · **Map:** [[Database Map]]
