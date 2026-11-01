---
tags: [concept, scope/in]
aliases: ["Service Quotas", "service quotas", "throttling"]
---

# Service Quotas and Throttling

**Service Quotas** are per-Region, per-account limits. Many can be raised on request, and the Service Quotas console shows usage.

- A DR Region needs matching quotas before a failover. Raise them in advance so a standby can scale.
- [[AWS Trusted Advisor]] and [[Amazon CloudWatch|CloudWatch]] alarms can warn when you near a quota.
- Throttling protects a service. Handle it with exponential backoff and jitter, or put a queue in front.
- [[Amazon API Gateway]] can throttle clients through usage plans.

## Exam tasks
- [[Task 2.2 Design highly available and or or fault-tolerant architectures]]

---
**Up:** [[Concepts Map]]
