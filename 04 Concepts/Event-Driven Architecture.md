---
tags: [concept, scope/in]
aliases: ["event-driven", "Event-driven architectures"]
---

# Event-Driven Architecture

Producers emit events and consumers react, without knowing about each other.

```mermaid
flowchart LR
    S3["S3 upload"] --> EB["EventBridge"]
    API["App event"] --> EB
    EB --> L["Lambda"]
    EB --> Q["SQS queue"]
    EB --> SF["Step Functions"]
```

Typical sources are [[S3 Event Notifications]], [[DynamoDB Streams]] and [[Amazon EventBridge]]. See [[SNS and SQS Fan-Out]].

## Exam tasks
- [[Task 2.1 Design scalable and loosely coupled architectures]]

---
**Up:** [[Concepts Map]]
