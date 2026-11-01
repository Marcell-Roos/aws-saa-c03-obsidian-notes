---
tags: [service, cat/front-end, scope/in]
aliases: ["API Gateway"]
---

# Amazon API Gateway

**Amazon API Gateway** is a fully managed service for developers to easily create, publish, maintain, monitor and secure APIs. It is serverless and scalable, supports RESTful APIs and WebSocket APIs. Has support for security, user authentication, API keys… We can validate requests and responses (also cache API responses). We pay only for the API calls we receive and the amount of data transferred out.

We can monitor API usage, latency, and error rates using [[Amazon CloudWatch|CloudWatch]].

**API Gateway Integrations**

- **[[AWS Lambda|Lambda]] Function** - can invoke AWS Lambda functions within our account and start [[AWS Step Functions]] state machines.
- **HTTP** - can make HTTP requests to endpoints hosted on AWS services such as [[AWS Elastic Beanstalk|Elastic Beanstalk]] and [[Amazon EC2|EC2]], as well as to non-AWS HTTP endpoints accessible over the public internet.
- **AWS Services** - can be directly integrated with other AWS services. For example, we can configure an API method to send data directly to [[Amazon Kinesis]].

**API Gateway Endpoint Types**

- **Edge-Optimized** (default) - for global clients. Requests are routed through the [[Amazon CloudFront|CloudFront]] Edge locations. The API Gateway still lives in only one region.
- **Regional** - for clients within the same region. Cloud manually combine with CloudFront (more control over the [[Caching Strategies|caching strategies]] and the distribution).
- **Private** - can only be accessed from our [[Amazon VPC|VPC]] using an interface VPC endpoint ([[Elastic Network Interface|ENI]]). We need to use a resource policy to define access.

**API Gateway Security**

**User authentication** through [[AWS IAM|IAM]] roles (for internal apps), cognito (for external users) or custom authorizer (our own logic).

**Lambda Authorizer** (Custom Authorizer) is a feature of AWS API Gateway that allows us to control access to our APIs using custom authentication and authorization logic implemented in AWS Lambda functions.

**Custom Domain Name HTTPS** security through integration with [[AWS Certificate Manager|ACM]]. If using Edge-Optimized endpoint, then the certificate must be in us-east-1. If using Regional endpoint, the certificate must be in the API Gateway region. We must setup CNAME or [[CNAME vs Alias Records|Alias record]] in [[Amazon Route 53|Route 53]].

**API types:** REST APIs have the most features, HTTP APIs are cheaper and simpler, and WebSocket APIs are for two-way messaging.

**Limits:** 29-second default integration timeout (it can be raised for Regional and private APIs), 10 MB payload, and a 10,000 requests per second account throttle.

## In this topic
- [[API Gateway Advanced Features]]
- [[API Gateway Authorizers and Integrations]]

## Exam tasks
- [[Task 2.1 Design scalable and loosely coupled architectures]]
- [[Task 4.4 Design cost-optimized network architectures]]

---
**Map:** [[Front-End Web and Mobile Map]]
