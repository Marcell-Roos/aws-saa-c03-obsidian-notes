---
tags: [concept, scope/in]
aliases: ["data lake", "data lakes"]
---

# Data Lakes

A central store of raw and processed data in any format, normally on [[Amazon S3]].

```mermaid
flowchart LR
    I["Kinesis, Firehose, DMS, DataSync"] --> S["S3 data lake"]
    S --> G["Glue crawlers and Data Catalog"]
    G --> A["Athena"]
    G --> R["Redshift Spectrum"]
    G --> E["EMR"]
    A --> Q["Amazon Quick dashboards"]
    LF["Lake Formation permissions"] -.-> S
```

Secure it with [[AWS Lake Formation]], [[S3 Access Control|bucket policies]], [[AWS KMS|KMS]] encryption and [[VPC Endpoints]] for ingestion.

## Exam tasks
- [[Task 3.5 Determine high-performing data ingestion and transformation solutions]]

---
**Up:** [[Concepts Map]]
