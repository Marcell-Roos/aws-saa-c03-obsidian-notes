---
tags: [service, cat/application, scope/in]
aliases: ["Fan Out", "fan out", "fan-out", "Fan-Out"]
---

# SNS and SQS Fan-Out

In the **Fan Out** pattern, we use [[Amazon SNS|SNS]] to broadcast messages to multiple [[Amazon SQS|SQS]] queues. Each queue can then be processed independently by separate consumers or applications. Need to configure SQS queue access policy to allow SNS to write.

It’s fully decoupled and we don't have data loss. We have ability to add more SQS subscribers over time. It works with SQS queues in other regions.

- **Solution Architecture - [[Amazon S3|S3]] Events to Multiple Queues.**

    For the same combination of event type and prefix we can only have one S3 Event rule. If we want to send the same S3 event to many SQS queues we should use fan out.

- **Solution Architecture - SNS to S3 through [[Amazon Data Firehose|KDF]].**

    SNS can send to [[Amazon Kinesis|Kinesis]] and we can have the following solutions architecture:

- **Solution Architecture - SNS FIFO + [[SQS FIFO Queues|SQS FIFO]] Fan Out.**

    In case we need fan out + ordering + deduplication.

- **Solution Architecture - Message Filtering.**

    JSON policy is used to filter messages sent to SNS topic’s subscriptions. If a subscription doesn’t have a filter policy, it receives every message.

## Exam tasks
- [[Task 2.1 Design scalable and loosely coupled architectures]]

---
**Up:** [[Amazon SNS]] · **Map:** [[Application Integration Map]]
