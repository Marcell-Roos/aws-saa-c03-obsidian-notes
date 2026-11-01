---
tags: [service, cat/application, scope/in]
aliases: ["SQS"]
---

# Amazon SQS

**SQS** is a fully managed message queuing service that enables us to [[Loose Coupling|decouple]] and scale microservices, distributed systems, and serverless applications.

There is no limit how many messages can be in the queue. Default retention of messages is 4 days, maximum of 14 days. Messages in the SQS queue will continue to exist even after the [[Amazon EC2|EC2 instance]] has processed it, until we delete that message. Consumers share the work to read messages and scale horizontally. It can have duplicate messages.

We can use SendMessage API by AWS SDK to produce messages. The message is **persisted** in SQS until a consumer deletes it.

Message consumers are running on EC2 instances, servers or [[AWS Lambda]]. They poll SQS for messages, process the messages and then delete them using DeleteMessage API.

Consumers receive and process messages in parallel and we can scale consumers horizontally to improve throughput of processing.

**SQS Security**

**Encryption** - has in-flight encryption using HTTPS, at-rest encryption using [[AWS KMS|KMS]] and we can do client-side encryption.

**Access Controls** - we can configure [[IAM Policy Structure|IAM policies]] to regulate access to the SQS API.

**SQS Access Policies** - similar to [[S3 Access Control|S3 bucket policies]]. Useful for [[Cross-Account Access|cross-account access]] to SQS queues. They allow other services to write to an SQS queue.

**Message size:** up to 1 MiB. Larger payloads go to [[Amazon S3|S3]] using the Extended Client Library. **Dead-letter queues** hold messages that fail repeatedly. **Delay queues** postpone delivery by up to 15 minutes.

## In this topic
- [[SQS FIFO Queues]]
- [[SQS Long Polling]]
- [[SQS Visibility Timeout]]
- [[SQS and Auto Scaling Patterns]]

## Exam tasks
- [[Task 2.1 Design scalable and loosely coupled architectures]]

---
**Map:** [[Application Integration Map]]
