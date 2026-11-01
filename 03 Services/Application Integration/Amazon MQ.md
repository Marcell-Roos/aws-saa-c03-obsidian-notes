---
tags: [service, cat/application, scope/in]
---

# Amazon MQ

When migrating to the cloud, instead of re-engineering the application to use [[Amazon SQS|SQS]] and [[Amazon SNS|SNS]], we can use Amazon MQ. **Amazon MQ** is a managed message broker service for RabbitMQ and ActiveMQ.

Amazon MQ doesn’t scale as much as SQS and SNS. Runs on servers but, can run in Multi-AZ with failover and has both queue feature (like SQS) and topic features (like SNS).

---
**Map:** [[Application Integration Map]]
