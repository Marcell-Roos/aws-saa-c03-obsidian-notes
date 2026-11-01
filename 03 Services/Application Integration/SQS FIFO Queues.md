---
tags: [service, cat/application, scope/in]
aliases: ["SQS FIFO", "FIFO queue", "FIFO queues", "FIFO Queue"]
---

# SQS FIFO Queues

In Standard [[Amazon SQS|SQS]] messages are processed in random order by the consumer. If we want ordering of messages in the queue there is **SQS FIFO Queue** variant. There messages are processed in order by the consumer.

Throughput is 300 TPS per API action, 3,000 with batching, and up to 70,000 in high-throughput mode in the largest Regions. FIFO gives exactly-once processing. The queue name must end in `.fifo`.

---
**Up:** [[Amazon SQS]] · **Map:** [[Application Integration Map]]
