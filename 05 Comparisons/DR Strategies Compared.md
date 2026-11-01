---
tags: [comparison, scope/in]
---

# DR Strategies Compared

The source had this only as an image.

| Strategy | [[RPO and RTO]] | Cost | What runs in DR |
| --- | --- | --- | --- |
| Backup and restore | Hours | Lowest | Backups only |
| Pilot light | Tens of minutes | Low | Core data replication |
| Warm standby | Minutes | Higher | Scaled-down full stack |
| Multi-site active-active | Near zero | Highest | Full stack |

```mermaid
flowchart LR
    A["Backup and restore"] --> B["Pilot light"] --> C["Warm standby"] --> D["Active-active"]
```

Moving right lowers RPO and RTO and raises cost. See [[Disaster Recovery Strategies]].

## Exam tasks
- [[Task 2.2 Design highly available and or or fault-tolerant architectures]]

---
**Up:** [[Comparisons Map]]
