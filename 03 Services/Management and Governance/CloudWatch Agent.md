---
tags: [service, cat/management, scope/in]
aliases: ["Unified Agent"]
---

# CloudWatch Agent

By default, no logs from our [[Amazon EC2|EC2 instance]] will go to [[Amazon CloudWatch|CloudWatch]], we need to run a CloudWatch Agent on EC2 to push the log files we want (need to make sure [[AWS IAM|IAM]] permissions are correct).

**[[CloudWatch Logs]] Agent** - old version of the agent. Can only send to CloudWatch Logs.

**CloudWatch Unified Agent** - it collects additional system-level metrics such as RAM, processes, etc. It collect logs to send them to CloudWatch Logs. It has centralized configuration using [[SSM Parameter Store]].

---
**Up:** [[Amazon CloudWatch]] · **Map:** [[Management and Governance Map]]
