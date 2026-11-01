---
tags: [service, cat/security, scope/in]
aliases: ["WAF"]
---

# AWS WAF

**AWS WAF (Web Application Firewall)** - protects our web applications from common web exploits (**Layer 7**). It can be deployed on **[[Application Load Balancer|ALB]], [[Amazon API Gateway|API Gateway]], [[Amazon CloudFront|CloudFront]], [[AWS AppSync|AppSync]]** and **[[Amazon Cognito|Cognito User Pool]]**.

On WAF we can define **[[WAF Rules|Web ACL]]** (Web Access Control List). Rules can include IP addresses, HTTP headers, HTTP body or URI strings. It can protect us from SQL Injection and XSS. There are Rate-based rules which are used for DDoS protection. A **rule group** is a reusable set of rules that we can add to a web ACL. Web ACL are regional except for CloudFront.

If we want to get a fixed IP in our application while using WAF with an ALB, we have to use [[AWS Global Accelerator|Global Accelerator]] to get fixed IP for application and then enable WAF on our ALB.

WAF also protects [[AWS App Runner|App Runner]] services, AWS Verified Access instances and [[AWS Amplify|Amplify]] apps. AWS WAF Classic reached end of support on 7 October 2026.

## In this topic
- [[WAF Rules]]

## Exam tasks
- [[Task 1.2 Design secure workloads and applications]]

---
**Map:** [[Security Identity and Compliance Map]]
