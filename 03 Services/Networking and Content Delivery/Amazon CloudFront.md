---
tags: [service, cat/networking, scope/in]
aliases: ["CloudFront"]
---

# Amazon CloudFront

**AWS CloudFront** is a Content Delivery Network (CDN) service. It delivers our content to end-users with low latency and high transfer speeds.. It improves read performance, content is cached at the [[AWS Global Infrastructure|edge location]]. When a user requests content, CloudFront serves it from the nearest edge location.

CloudFront integrates with [[AWS Shield]] for DDoS protection, AWS Web Application Firewall ([[AWS WAF|WAF]]) to protect against common web exploits, and SSL/TLS encryption to secure data transfer.

**Also available:** [[Amazon VPC|VPC]] origins let CloudFront reach [[Application Load Balancer|ALBs]], [[Network Load Balancer|NLBs]] and [[Amazon EC2|EC2]] in private subnets, so the origin needs no public exposure.

## In this topic
- [[CloudFront Cache Invalidation]]
- [[CloudFront Functions and Lambda@Edge]]
- [[CloudFront Geo Restriction]]
- [[CloudFront Origins]]
- [[CloudFront Price Classes]]
- [[CloudFront Signed URLs and Cookies]]

## Exam tasks
- [[Task 2.1 Design scalable and loosely coupled architectures]]
- [[Task 3.4 Determine high-performing and or or scalable network architectures]]
- [[Task 4.4 Design cost-optimized network architectures]]

---
**Map:** [[Networking and Content Delivery Map]]
