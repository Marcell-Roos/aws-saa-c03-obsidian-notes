---
tags: [service, cat/storage, scope/in]
---

# S3 Event Notifications

**S3 Event Notifications** allow us to receive notifications when certain events happen to objects within our [[Amazon S3|S3 buckets]]. We can create as many S3 events as desired.

S3 event notifications typically deliver events in seconds but can sometimes take a minute or longer.

We can directly send S3 events to [[Amazon EventBridge|EventBridge]], expanding the range of destinations and enabling more complex event handling and routing scenarios. [[SQS FIFO Queues|SQS FIFO]] queues aren't supported as an S3 event notification destination.

- Advanced filtering options with JSON rules.
- Multiple destinations ([[AWS Step Functions|Step Functions]], [[Amazon Kinesis|Kinesis]] Streams)
- Archive and replay events.

---
**Up:** [[Amazon S3]] · **Map:** [[Storage Map]]
