---
tags: [service, cat/serverless, scope/in]
aliases: ["Lambda", "Lambda function", "Lambda functions", "AWS Lambda functions"]
---

# AWS Lambda

**AWS Lambda** lets us run virtual functions on-demand (serverless). It has short execution and automated scaling. Functions get invoked by AWS only when needed (Event-Driven). Lambda functions are **[[Stateless and Stateful Workloads|stateless]]**, meaning each invocation is independent of previous invocations. State can be managed via external storage like [[Amazon DynamoDB|DynamoDB]] or [[Amazon S3|S3]].

It is is integrated with the whole AWS suite of services and many programming languages. We can easily monitor AWS Lambda through AWS [[Amazon CloudWatch|CloudWatch]].

We **pay per request and compute time**. 1 million requests per month and 400 000 GB-seconds of compute time per month are free.

Lambda can be used for serverless CRON job (trigger an event at specific time).

Docker images can be run using Lambda. The container image must implement the Lambda Runtime API. We can't run Windows containers (only Linux).

**AWS Lambda Layers** - we can configure our AWS Lambda function to pull in additional code and content in the form of layers. A layer is a ZIP archive that contains libraries, a custom runtime, or other dependencies. With layers, we can use libraries in our function without needing to include them in your deployment package.

**AWS Lambda URLs** are a feature that allows us to create HTTP endpoints for our Lambda functions. This makes it easier to build serverless applications that interact with web clients or other HTTP-based services.

**Lambda Limits**

Since AWS Lambda functions can scale extremely quickly, it's a good idea to deploy a Amazon CloudWatch Alarm that notifies our team when function metrics such as ConcurrentExecutions or Invocations exceeds the expected threshold.

**Limits** (the source had these only as an image):

| Setting | Limit |
| --- | --- |
| Memory | 128 MB to 10,240 MB, and CPU scales with memory |
| Timeout | 15 minutes |
| /tmp | 512 MB to 10,240 MB |
| Deployment package | 50 MB zipped, 250 MB unzipped, 10 GB container image |
| Payload | 6 MB sync, 1 MB async, 200 MB streamed |
| Environment variables | 4 KB |
| Layers | 5 |
| Concurrency | 1,000 per Region by default |
| Scaling rate | 1,000 execution environments every 10 seconds per function |

**Newer options:** AWS docs now list Lambda Managed Instances, durable functions, Lambda MicroVMs and Lambda Web Functions. They aren't in the exam guide.

## In this topic
- [[Lambda Concurrency]]
- [[Lambda Invocation Models]]
- [[Lambda SnapStart]]
- [[Lambda in a VPC]]

## Exam tasks
- [[Task 2.1 Design scalable and loosely coupled architectures]]
- [[Task 3.2 Design high-performing and elastic compute solutions]]

---
**Map:** [[Serverless Map]]
