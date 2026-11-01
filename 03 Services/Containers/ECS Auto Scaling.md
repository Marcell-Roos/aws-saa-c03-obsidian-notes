---
tags: [service, cat/containers, scope/in]
---

# ECS Auto Scaling

With **ECS Auto Scaling** we can automatically increase/decrease the desired number of [[Amazon ECS|ECS tasks]]. [[AWS Fargate|Fargate]] Auto Scaling is much easier to setup because it is Serverless.

ECS Auto Scaling is similar but not equal to [[Amazon EC2 Auto Scaling|EC2 Auto Scaling]] (task level vs instance level).

- **[[ASG Scaling Policies|Target Tracking]] Scaling** - scale based on target value for a specific [[Amazon CloudWatch|CloudWatch]] metric.
- **Step Scaling** - scale based on a specified [[CloudWatch Alarms|CloudWatch Alarm]].
- **Scheduled Scaling** - scale based on a specified date/time (predictable changes).

For [[Amazon EC2|EC2]] launch type we can accommodate ECS scaling by adding underlying EC2 instances (using ASG or ECS Cluster Capacity Provider). ECS Cluster Capacity Provider is better.

---
**Up:** [[Amazon ECS]] · **Map:** [[Containers Map]]
