---
tags: [service, cat/cost, scope/unlisted]
aliases: ["Cost Anomaly Detection"]
---

# AWS Cost Anomaly Detection

> [!note] Exam scope
> Not on AWS's in-scope or out-of-scope list. The in-scope list is non-exhaustive, so treat this as background.

**Cost Anomaly Detection** continuously monitor our cost and usage using ML to detect unusual spends. It learns our unique, historic spend patterns to detect one-time cost spike and/or continous cost increases (we don't need to define thresholds).

We can monitor AWS services, member accounts, [[Cost Allocation Tags|cost allocation tags]] or cost categories. It will send us anomaly detection report with root-cause analysis and we can get notified with alerts using [[Amazon SNS|SNS]].

---
**Map:** [[Cost Management Map]]
