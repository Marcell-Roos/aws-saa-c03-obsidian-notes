---
tags: [comparison, scope/in]
aliases: ["SQS vs SNS vs Kinesis"]
---

# SQS vs SNS vs Kinesis vs EventBridge

The source had the core comparison only as an image.

| | [[Amazon SQS]] | [[Amazon SNS]] | [[Kinesis Data Streams]] | [[Amazon EventBridge]] |
| --- | --- | --- | --- | --- |
| Model | Queue, consumers pull | Pub/sub, pushes | Stream, consumers pull | Event bus, pushes by rule |
| Consumers | Competing, each message handled once | Every subscriber gets a copy | Many independent readers | Rule targets |
| Persistence | Up to 14 days | None | 1 to 365 days | Optional archive |
| Replay | No | No | Yes | Yes, from an archive |
| Ordering | [[SQS FIFO Queues\|FIFO queues]] | FIFO topics | Per shard | No |
| Scaling | Automatic | Automatic | Shards, or on-demand | Automatic |
| Max message | 1 MiB | 256 KiB by default, up to 1 MiB | 10 MiB record | See [[Amazon EventBridge]] |
| Use for | Buffering, worker pools | Notifications, [[SNS and SQS Fan-Out\|fan-out]] | Real-time analytics | SaaS and AWS event routing |

---
**Up:** [[Comparisons Map]]
