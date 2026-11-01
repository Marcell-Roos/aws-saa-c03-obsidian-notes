---
tags: [service, cat/migration, scope/in]
aliases: ["Full Load", "Replication Instance", "CDC"]
---

# DMS Replication Details

A **replication instance** runs **replication tasks** between source and target endpoints.

| Migration type | What it does |
| --- | --- |
| Full load | Copies existing data |
| Full load + CDC | Copies, then keeps changes flowing, for minimal downtime |
| CDC only | Replicates ongoing changes |

Use AWS SCT or [[AWS DMS|DMS]] Schema Conversion for **heterogeneous** migrations, and skip schema conversion for homogeneous ones. See [[RDS and Aurora Migrations]].

---
**Up:** [[AWS DMS]] · **Map:** [[Migration and Transfer Map]]
