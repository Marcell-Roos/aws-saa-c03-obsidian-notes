---
tags: [service, cat/management, scope/in]
aliases: ["custom metrics", "Metric Streams"]
---

# CloudWatch Metrics

**[[Amazon CloudWatch|CloudWatch]]** provides metrics for every service in AWS. Metric is a variable to monitor (CPU Utilization, Network In, etc). We can create custom metrics too (**Memory Utilization**).

Each metric has timestamps and dimension. **Dimension** is an attribute of a metric (instance id, environment, etc.). CloudWatch can create dashboards of metrics.

**CloudWatch Metric Streams** - continually stream CloudWatch metrics to a destination of our choice, with near real-time delivery and low latency. We can use [[Amazon Data Firehose|KDF]] or third party service provider (Datadog, Dynatrace, etc). We have option to filter metrics to only stream a subset of them.

---
**Up:** [[Amazon CloudWatch]] · **Map:** [[Management and Governance Map]]
