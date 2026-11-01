---
tags: [service, cat/management, scope/unlisted]
aliases: ["Trusted Advisor"]
---

# AWS Trusted Advisor

> [!note] Exam scope
> Not on AWS's in-scope or out-of-scope list. The in-scope list is non-exhaustive, so treat this as background.

**Trusted Advisor** is a service that helps customers optimize their AWS environments, improve performance, and save money. It provides real-time guidance to help users follow AWS best practices.

It lets us analyze our AWS accounts and provides recommendation on six categories:

- Cost optimization.
- Performance.
- Security.
- Fault tolerance.
- Service limits.
- Operational Excellence.

For Business Support+, Enterprise Support and Unified Operations plans:

- Full Set of Checks.
- Programmatic Access using AWS Support API.
- **Solution Architecture - Quota Monitor.**

    Pattern uses an [[AWS Lambda]] function that runs once every 24 hours. The Lambda function refreshes the AWS Trusted Advisor Service Limits checks to retrieve the most current utilization and quota data through API calls. [[Amazon CloudWatch]] Events captures the status events from Trusted Advisor. It uses a set of [[Amazon EventBridge|CloudWatch Events]] rules to send the status events to all the targets we choose during initial deployment of the solution: [[Amazon SQS|SQS]] queue, [[Amazon SNS|SNS]] topic or a Lambda function for Slack notifications.

The Basic plan gets Service Limits checks plus selected Security and Fault tolerance checks. Developer, Business and Enterprise On-Ramp plans end on 1 January 2027.

---
**Map:** [[Management and Governance Map]]
