---
tags: [service, cat/application, scope/in]
aliases: ["Step Functions"]
---

# AWS Step Functions

**Step Functions** is a serverless orchestration service that allows us to coordinate multiple AWS services into serverless workflows. It orchestrates our [[AWS Lambda|Lambda functions]].

It can be integrated with [[Amazon EC2|EC2]], [[Amazon ECS|ECS]], on-remises servers, [[Amazon API Gateway|API Gateway]], [[Amazon SQS|SQS]], etc …

We can use it for implementing human approval feature.

**Step Functions Local** let us test state machines on a development machine, but AWS now marks it as unsupported.

See [[Standard vs Express Workflows]].

**Error handling:** `Retry` and `Catch` fields handle failures in the state machine rather than in code.

## In this topic
- [[Amazon SWF]]
- [[Step Functions Map State]]

## Exam tasks
- [[Task 2.1 Design scalable and loosely coupled architectures]]

---
**Map:** [[Application Integration Map]]
