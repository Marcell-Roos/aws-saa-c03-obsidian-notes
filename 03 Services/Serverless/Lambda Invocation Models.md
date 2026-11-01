---
tags: [service, cat/serverless, scope/in]
aliases: ["Invocation Types"]
---

# Lambda Invocation Models

| Model | Examples | Retry behaviour |
| --- | --- | --- |
| Synchronous | [[Amazon API Gateway]], [[Application Load Balancer\|ALB]] | The caller handles errors |
| Asynchronous | [[Amazon S3]] events, [[Amazon SNS]], [[Amazon EventBridge\|EventBridge]] | [[AWS Lambda\|Lambda]] retries twice, then a dead-letter queue or destination |
| Event source mapping | [[Amazon SQS]], [[Kinesis Data Streams]], [[DynamoDB Streams]] | Lambda polls the source |

---
**Up:** [[AWS Lambda]] · **Map:** [[Serverless Map]]
