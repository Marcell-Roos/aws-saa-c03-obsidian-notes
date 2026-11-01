---
tags: [service, cat/security, scope/in]
aliases: ["Cognito", "Cognito User Pools", "Cognito Identity Pools", "Cognito User Pool"]
---

# Amazon Cognito

**Cognito** gives users an identity to interact with our web or mobile applications.

- **Cognito User Pools (CUP)** - serverless database of user for our web & mobile apps. It provides sign in functionality for app users. Integration with **[[Amazon API Gateway|API Gateway]], [[AWS AppSync|AppSync]]** & **[[Application Load Balancer|ALB]]**. It provides simple login (username/mail and password combination), password reset, 2FA, [[IAM Password Policy and MFA|MFA]]…

- **Cognito Identity Pools (Federated Identity)** - used to get identities for “users” so they obtain temporary AWS credentials. Users source can be CUP, third party logins, etc…

    Users can then access AWS services directly or through API Gateway. The [[IAM Policy Structure|IAM policies]] applied to the credentials are defined in Cognito. There are default [[AWS IAM|IAM]] roles for authenticated and guest users.

**Row Level Security in [[Amazon DynamoDB|DynamoDB]]**

An IAM policy condition `dynamodb:LeadingKeys` limits users to items whose [[Data Ordering in Kinesis and SQS FIFO|partition key]] equals their Cognito identity ID.

## Exam tasks
- [[Task 1.2 Design secure workloads and applications]]

---
**Map:** [[Security Identity and Compliance Map]]
