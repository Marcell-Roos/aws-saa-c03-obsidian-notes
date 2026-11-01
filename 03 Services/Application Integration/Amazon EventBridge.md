---
tags: [service, cat/application, scope/in]
aliases: ["EventBridge", "Event Bridge", "CloudWatch Events"]
---

# Amazon EventBridge

**EventBridge** is a serverless event bus service that makes it easy to connect applications using data from our own applications, integrated SaaS applications, and AWS services.

We can schedule events with CRON jobs or we can make event rules to react to a service doing something. Also it’s possible to trigger [[AWS Lambda|Lambda functions]], send [[Amazon SQS|SQS]]/SNS messages …

**EventBridge Schema Registry** - allows us to generate code for our application, that will know in advance how data is structured in the event bus. Schema can be versioned.

**Event Bus Types**

Event buses can be accessed by other AWS accounts using [[Resource-based Policies vs IAM Roles|resource-based policies]].

**Resource-based Policy** - manages permissions for a specific Event Bus. It is used to aggregate all events from our AWS Organization in a single AWS account or AWS region.

We can archive events sent to an event bus (indefinitely or set period) and we can replay archived events.

**Bus types:** default (AWS services), partner (SaaS) and custom. The source had this only as an image. **EventBridge Scheduler** runs one-off or recurring tasks. **Pipes** connect a source to a target with filtering and enrichment.

## Exam tasks
- [[Task 2.1 Design scalable and loosely coupled architectures]]

---
**Map:** [[Application Integration Map]]
