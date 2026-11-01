---
tags: [architecture, scope/in]
---

# Case Study Microservices

We are free to design each [[Microservices|microservice]] the way we want.

Synchronous patterns: [[Amazon API Gateway|API Gateway]], Load Balancers.

Asynchronous patterns: [[Amazon SQS|SQS]], [[Amazon Kinesis|Kinesis]], [[Amazon SNS|SNS]], [[AWS Lambda|Lambda]].

Challenges with microservices:

- Repeated overhead for creating each new microservice.
- Issues with optimizing server density/utilization.
- Complexity of running multiple versions of multiple microservices simultaneously.

Challenges solved by serverless patterns:

- API Gateway, Lambda scale automatically and we can pay per usage.
- We can easily clone API and reproduce environments.

---
**Up:** [[Architecture Patterns]]
