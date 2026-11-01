---
tags: [concept, scope/in]
aliases: ["partition key", "Partition Key"]
---

# Data Ordering in Kinesis and SQS FIFO

To ensure ordering for specific types of data in [[Kinesis Data Streams|KDS]], we can use partition keys. Events with the same partition key are routed to the same shard, and thus will be read in order.

For [[SQS FIFO Queues|SQS FIFO]], if we don't use a Group ID, messages are consumed in the order they are sent, with only one consumer.

If we want to scale the number of consumers, but want messages to be “grouped” when they are related to each other, then we should use a Group ID (similar to Partition Key in [[Amazon Kinesis|Kinesis]]).

Lets assume 100 trucks, 5 kinesis shards, 1 SQS FIFO:

---
**Up:** [[Amazon Kinesis]]
