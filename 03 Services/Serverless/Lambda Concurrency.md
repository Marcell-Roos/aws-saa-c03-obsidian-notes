---
tags: [service, cat/serverless, scope/in]
aliases: ["Provisioned Concurrency", "Reserved Concurrency"]
---

# Lambda Concurrency

We can configure number of [[AWS Lambda|Lambda function]] which will execute simultaneously. Lambda automatically scales our function by running multiple instances of our code in parallel to handle high volumes of requests.

- **Provisioned Concurrency** - specified number of function instances are **pre-warmed** and ready to handle requests, which helps reduce latency and avoid cold starts. It’s useful for functions with predictable traffic patterns or **latency-sensitive** applications.
- **Reserved Concurrency** - allows us to allocate a specific number of concurrent executions for a Lambda function, which ensures that the function always has the specified number of concurrent executions available and controls its maximum concurrency.

The exam distinction: **Reserved** caps and guarantees concurrency, with no extra charge. **Provisioned** keeps environments warm and costs extra.

## Exam tasks
- [[Task 3.2 Design high-performing and elastic compute solutions]]

---
**Up:** [[AWS Lambda]] · **Map:** [[Serverless Map]]
