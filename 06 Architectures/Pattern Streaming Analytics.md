---
tags: [architecture, scope/in]
---

# Pattern Streaming Analytics

```mermaid
flowchart LR
    D["Devices"] --> K["Kinesis Data Streams"]
    K --> F["Managed Flink"]
    K --> FH["Data Firehose"]
    FH --> S["S3"]
    S --> A["Athena"]
    A --> Q["Amazon Quick"]
    K --> L["Lambda"]
    L --> DB["DynamoDB"]
```

See [[Case Study Big Data Ingestion Pipeline]].

## Exam tasks
- [[Task 3.5 Determine high-performing data ingestion and transformation solutions]]

---
**Up:** [[Architecture Patterns]]
