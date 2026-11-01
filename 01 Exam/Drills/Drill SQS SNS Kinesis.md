---
tags: [drill, scope/in]
---

# Drill SQS SNS Kinesis

Adapted from [RonitSachdev/aws-saa-c03-guides](https://github.com/RonitSachdev/aws-saa-c03-guides) (CC BY 4.0), with outdated facts changed.

## Question patterns

- *"Web tier overwhelmed by traffic spikes; orders being lost"* → **[[Amazon SQS|SQS]] + Auto Scaling worker group** (queue buffers the spike, workers scale on depth)
- *"Messages must be processed in strict order with no duplicates"* → **[[SQS FIFO Queues|SQS FIFO]]** (order + exactly-once; remember 300/3,000 msg/s cap)
- *"One event must notify three downstream systems, and none may miss it even if temporarily down"* → **[[Amazon SNS|SNS]] [[SNS and SQS Fan-Out|fan-out]] to multiple SQS queues** (queues hold messages for sleeping services)
- *"Some SQS messages are being processed twice"* → **Increase the [[SQS Visibility Timeout|visibility timeout]]** (processing outlasts the hiding window)
- *"Messages that repeatedly fail are blocking the queue"* → **Dead-Letter Queue with MaxReceiveCount** (quarantine poison messages)
- *"Clickstream analytics: two applications must consume the same real-time data, with ability to reprocess yesterday"* → **[[Kinesis Data Streams]]** (multiple consumers + replay = its two kill-shots)
- *"Stream IoT telemetry into [[Amazon S3|S3]] with the least operational overhead, no custom code"* → **[[Amazon Data Firehose]]** (zero-code delivery truck to S3)
- *"Reduce cost of consumers polling an often-empty queue"* → **Long polling (20s)** (fewer empty receives)
- *"Migrate an on-prem RabbitMQ/ActiveMQ app using AMQP/JMS/MQTT without rewriting"* → **[[Amazon MQ]]** (protocol names = MQ)
- *"Message payloads are 5 MB, exceeding the SQS limit"* → **Store in S3, send a pointer** (1 MiB cap)
- *"Each subscriber should only receive certain message types from a topic"* → **SNS message filtering** (filter policy per subscription)

## Pocket card

| Keyword | Answer |
|---|---|
| Decouple / buffer spikes | SQS |
| One message → one worker, PULL | SQS |
| Processed twice | Increase visibility timeout (default 30s) |
| Poison messages | DLQ + MaxReceiveCount |
| Empty-poll cost | Long polling (20s) |
| Strict order + exactly-once | FIFO (300 / 3,000 msg/s) |
| Message > 1 MiB | S3 + pointer |
| Retention | 4 days default / 14 max |
| One → many, PUSH, instant | SNS (stores nothing) |
| Notify many, durably | SNS → multiple SQS (fan-out) |
| Multiple consumers, same data, replay | Kinesis Data Streams (24h–365d) |
| Shard throughput | 1 MB/s in, 2 MB/s out, order per shard |
| Stream → S3, zero code, ~60s | Firehose (S3/Redshift/OpenSearch/Splunk) |
| MQTT / AMQP / JMS / RabbitMQ | Amazon MQ |
| Workers scale on queue depth | [[Amazon EC2 Auto Scaling\|ASG]] + [[Amazon CloudWatch\|CloudWatch]] queue metric |

---
**Up:** [[Drills Map]]
