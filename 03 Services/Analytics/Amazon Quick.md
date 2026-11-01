---
tags: [service, cat/analytics, scope/in]
aliases: ["QuickSight", "Quicksight", "Quick Sight", "Amazon QuickSight"]
---

# Amazon Quick

**Amazon Quick Sight** (now part of **Amazon Quick**, formerly Amazon QuickSight) is a serverless ML-powered business intelligence service to create interactive dashboards. It is fast, automatically scalable, embeddable, with per-session pricing. Can be integrated with [[Amazon RDS|RDS]], [[Amazon Aurora|Aurora]], [[Amazon Athena|Athena]], [[Amazon Redshift|Redshift]] …

It has in-memory computation capabilities using SPICE engine. In enterprise edition we have possibility to setup Column-Level Security (CLS) to prevent some columns to be displayed to users who don't have permission.

Usage: business analytics, building visualizations, perform ad-hoc analysis …

In QuickSight we can define users (standard versions) and groups (enterprise version). These users and groups only exist within QuickSight, not [[AWS IAM|IAM]]!

**Dashboard** - read-only snapshot of an analysis that we can share. It preserves the configuration of the analysis.

We can share the analysis or the dashboard with users or groups. Users who see the dashboard can also see the underlying data.

Amazon Quick also includes AI agents and Quick Flows. For the exam, the BI dashboards part matters most.

## Exam tasks
- [[Task 3.5 Determine high-performing data ingestion and transformation solutions]]

---
**Map:** [[Analytics Map]]
