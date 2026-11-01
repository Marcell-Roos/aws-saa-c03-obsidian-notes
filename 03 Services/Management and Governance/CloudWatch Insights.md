---
tags: [service, cat/management, scope/in]
aliases: ["Container Insights", "Lambda Insights", "Contributor Insights", "Application Insights"]
---

# CloudWatch Insights

**[[Amazon CloudWatch|CloudWatch]] Container Insights** - used to collect, aggregate and summarize metrics and logs from containers. In [[Amazon EKS|EKS]] and Kubernetes, CloudWatch Insights is using a containered version of the [[CloudWatch Agent]] to discover containers.

**CloudWatch Lambda Insights** - monitoring and troubleshooting solution for serverless applications running on [[AWS Lambda]]. It collects, aggregates and summarizes system-level metrics and diagnostic information (cold starts, Lambda worker shutdowns).

**CloudWatch Contributor Insights** - analyzes log data and creates time series that display contributor data. We can see metrics about the top-N contributors. It helps us to find top talkers and understand who or what is impacting system performance. We can build our rules from scratch or we can also use sample rules that AWS has created.

Use cases: find bad hosts, identify the heaviest network users or find the URLs that generate the most errors.

**CloudWatch Application Insights** - provides automated dashboards that show potential problems with monitored applications to help isolate ongoing issues. It is powered by [[Amazon SageMaker AI|SageMaker]].

It gives us enhanced visibility into our application health to reduce the time it will take us to troubleshoot and repair our applications. Findings and alerts are sent to [[Amazon EventBridge|EventBridge]] and [[AWS Systems Manager|SSM]] OpsCenter.

---
**Up:** [[Amazon CloudWatch]] · **Map:** [[Management and Governance Map]]
