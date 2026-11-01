---
tags: [service, cat/networking, scope/in]
aliases: ["Health Checks"]
---

# Route 53 Health Checks

HTTP Health Checks are only for public resources. With health checks we get automated [[DNS Fundamentals|DNS]] failover. Health checks can be integrated with [[Amazon CloudWatch|CloudWatch]] metrics.

- Health Checks that monitor an endpoint

    About 15 global health checkers will check the endpoint health. If more than 18% of health checkers report the endpoint is healthy, [[Amazon Route 53|Route 53]] considers it Healthy.

    They pass only when the endpoint responds with the 2xx and 3xx status codes. Health checks can be setup to pass/fail based on the text in the first 5120 bytes of the response.

    To make it work we must configure our router/firewall to allow incoming requests from Route 53 Health Checkers.

- Calculated Health Checks

    It combines the results of multiple health checks into a single health check. We can use OR, AND or NOT operators and can specify how many of the health checks need to pass to make the parent pass.

    It is used to perform maintenance to our website without causing all health checks to fail.

- Health Checks that monitor [[CloudWatch Alarms]] (**full control,** for private resources).

    Because health checkers are outside the [[Amazon VPC|VPC]], they can't access private endpoints. We can create CloudWatch Metric and associate a CloudWatch Alarm, then create a health check that checks the alarm itself.

## Exam tasks
- [[Task 2.2 Design highly available and or or fault-tolerant architectures]]

---
**Up:** [[Amazon Route 53]] · **Map:** [[Networking and Content Delivery Map]]
