---
tags: [service, cat/compute, scope/in]
aliases: ["scaling policies", "Scaling Policies", "target tracking", "Target Tracking", "Predictive Scaling"]
---

# ASG Scaling Policies

- **Manual Scaling** - Update the size of an [[Amazon EC2 Auto Scaling|ASG]] manually. Suitable for predictable workloads where we can manually scale based on known traffic patterns.
- **Dynamic Scaling** - Respond to changing demand.
    - **Simple/Step Scaling**

        Useful for applications with variable demand where we need more granular control over scaling actions.

        Example: When a [[Amazon CloudWatch|CloudWatch]] alarm is triggered (example CPU > 70%), then add more units. When CloudWatch alarm is triggered (example CPU < 30%), then remove unit.

    - **Target Tracking Scaling**

        Simplifies scaling by allowing us to set a desired target value for a specific metric, making it ideal for applications with varying demand and performance requirements. Example: If we want the average ASG CPU to stay at around 40%.

    - **Scheduled Scaling**

        Ideal for applications with predictable traffic patterns, such as regular business hours or batch processing jobs. Example: Increase the min capacity to 10 at 5PM on Fridays.

    - **Predictive Scaling** - Uses ML to predict future traffic ahead of time. Automatically provisions the right number of [[Amazon EC2|EC2 instances]] in advance. Suitable for applications with periodic, predictable load changes, allowing us to proactively scale and avoid latency or over-provisioning.

Good metrics to scale on:

- **CPU Utilization** (average CPU utilization across our instances).
- **Request Count Per Target**.

- **Average Network In/Out**.
- **Any custom metric** (that we post using CloudWatch).

**Scaling Cooldown** - after a scaling activity happens, we are in the cooldown period (default 300s, and it only applies to simple scaling policies). During the cooldown period, the ASG will not launch or terminate additional instances (to allow for metrics to stabilize).

Good practice is to use a ready-to-use [[Amazon Machine Image|AMI]] to reduce configuration time in order to be serving request faster and reduce the cooldown period.

## Exam tasks
- [[Task 3.2 Design high-performing and elastic compute solutions]]

---
**Up:** [[Amazon EC2 Auto Scaling]] · **Map:** [[Compute Map]]
