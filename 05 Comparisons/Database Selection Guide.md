---
tags: [comparison, scope/in]
---

# Database Selection Guide

```mermaid
flowchart TD
    Q{"Data model?"}
    Q -->|"Relational OLTP"| R{"Need cloud-native scale?"}
    R -->|"Yes"| A["Aurora"]
    R -->|"No"| RD["RDS"]
    Q -->|"Key-value at any scale"| D["DynamoDB"]
    Q -->|"Analytics"| RS["Redshift"]
    Q -->|"Graph"| N["Neptune"]
    Q -->|"Document, MongoDB"| DD["DocumentDB"]
    Q -->|"Cassandra"| K["Keyspaces"]
    Q -->|"Time series"| T["Timestream"]
    Q -->|"Cache"| EC["ElastiCache"]
    Q -->|"Search"| O["OpenSearch"]
```

Keywords: "heterogeneous migration" points to [[AWS DMS]]. "Too many connections" points to [[RDS Proxy]].

## Exam tasks
- [[Task 3.3 Determine high-performing database solutions]]
- [[Task 4.3 Design cost-optimized database solutions]]

---
**Up:** [[Decision Guides Map]]
