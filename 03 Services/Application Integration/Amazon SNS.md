---
tags: [service, cat/application, scope/in]
aliases: ["SNS"]
---

# Amazon SNS

**SNS** is a topic-based publisher/subscriber model. The event publishers only sends message to one SNS topic. Subscribers receive messages by subscribing to a topic. Subscribers can be various endpoints such as email, SMS, [[AWS Lambda|AWS Lambda functions]]. Each subscriber to the topic will get all the messages.

- **Topic Publish** - using SDK. First create topic, then create a subscription and publish to the topic.
- **Direct Publish** - for mobile apps SDK. We need to create a platform application and platform endpoint. Then publish to the platform endpoint.

**SNS Message Filtering** - assign a filter policy to the topic subscription, and the subscriber will only receive a message that they are interested in.

SNS has **FIFO Topic** (ordering of messages in the topic). It has similar features as [[SQS FIFO Queues|SQS FIFO]]:

- **Ordering** by Message Group ID.
- **Deduplication** using a Deduplication ID or Content Based Deduplication.

Both [[Amazon SQS|SQS]] Standard and FIFO queues can be subscribers.

**SNS Security**

**Encryption** - has in-flight encryption using HTTPS, at-rest encryption using [[AWS KMS|KMS]] and we can do client-side encryption.

**Access Controls** - we can configure [[IAM Policy Structure|IAM policies]] to regulate access to the SNS API.

**SNS Access Policies** - similar to [[S3 Access Control|S3 bucket policies]]. Useful for [[Cross-Account Access|cross-account access]] to SNS topics. They allow other services to write to an SNS topic.

Default maximum message size is 256 KiB, and it can be raised to 1 MiB per topic. Standard topics give best-effort ordering. FIFO topics deliver to SQS FIFO and standard queues.

## In this topic
- [[SNS and SQS Fan-Out]]

## Exam tasks
- [[Task 2.1 Design scalable and loosely coupled architectures]]

---
**Map:** [[Application Integration Map]]
