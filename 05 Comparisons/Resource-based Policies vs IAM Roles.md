---
tags: [comparison, scope/in]
aliases: ["resource-based policy", "resource-based policies", "Resource-based Policy"]
---

# Resource-based Policies vs IAM Roles

When we want to perform an API call on a [[Amazon S3|S3 bucket]] cross account we have two options. Attaching a resource-based policy to a resource (e.g. S3 bucket policy) or using a role as a proxy.

- When we assume a role (user, application or service), we give up our original permissions and take the permissions assigned to the role.
- When using a resource-based policy, the principal doesn't have to give up his permissions.

> User in account A needs to scan a [[Amazon DynamoDB|DynamoDB]] table in account A and dump it in an S3 bucket in account B. ⇒ we should use resource-based policy.

It is really important when we use [[Amazon EventBridge|EventBridge]]. When rule runs, it needs permissions on the target.

We have targets that support resource-based policy (**[[AWS Lambda]], [[Amazon SNS|SNS]], [[Amazon SQS|SQS]], S3 buckets, [[Amazon API Gateway|API Gateway]]**) and targets that supports [[IAM Users Groups and Roles|IAM role]] (**[[Amazon Kinesis|Kinesis]] stream, [[SSM Run Command]], [[Amazon ECS|ECS]] task**).

## Exam tasks
- [[Task 1.1 Design secure access to AWS resources]]

---
**Up:** [[AWS IAM]]
