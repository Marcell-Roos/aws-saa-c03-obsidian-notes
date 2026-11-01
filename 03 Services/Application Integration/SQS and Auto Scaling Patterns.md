---
tags: [service, cat/application, scope/in]
---

# SQS and Auto Scaling Patterns

**Scale Based on [[CloudWatch Alarms|CloudWatch Alarm]]**

An alarm on queue depth (`ApproximateNumberOfMessages`) triggers [[Amazon EC2 Auto Scaling|ASG]] scaling, so workers match the backlog.

**Buffer to Database Writes**

Writes go to [[Amazon SQS|SQS]] first, and workers write to the database at a safe rate, so a spike can't overload it or lose transactions.

**Decouple between Application Tiers**

The front end puts jobs on a queue and a separate back-end ASG processes them, so each tier scales alone. See [[Pattern Queue-Based Load Leveling]].

---
**Up:** [[Amazon SQS]] · **Map:** [[Application Integration Map]]
