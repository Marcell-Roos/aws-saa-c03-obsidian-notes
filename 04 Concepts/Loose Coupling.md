---
tags: [concept, scope/in]
aliases: ["loosely coupled", "decoupling", "decouple"]
---

# Loose Coupling

Components interact through a buffer or interface, so one can fail or scale without affecting the others.

- **Queue:** [[Amazon SQS]] absorbs spikes and lets workers scale on their own.
- **Pub/sub:** [[Amazon SNS]] delivers to many subscribers.
- **Event bus:** [[Amazon EventBridge]] routes events by content.
- **Stream:** [[Kinesis Data Streams]] for ordered, replayable data.
- **Load balancer:** [[Elastic Load Balancing]] hides individual instances.

See [[SQS vs SNS vs Kinesis vs EventBridge]].

## Exam tasks
- [[Task 2.1 Design scalable and loosely coupled architectures]]

---
**Up:** [[Concepts Map]]
