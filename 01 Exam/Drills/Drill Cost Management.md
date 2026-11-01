---
tags: [drill, scope/in]
---

# Drill Cost Management

Adapted from [RonitSachdev/aws-saa-c03-guides](https://github.com/RonitSachdev/aws-saa-c03-guides) (CC BY 4.0), with outdated facts changed.

## Question patterns

- *"Receive a notification when forecasted spend reaches 80% of the monthly budget"* → **[[AWS Budgets]]** (threshold + notify = Budgets, every time)
- *"Finance needs to attribute AWS costs to individual teams and projects"* → **[[Cost Allocation Tags]]** (tag, activate in billing, slice the bill)
- *"Analysts need the most granular billing data, queryable with standard SQL"* → **[[AWS Cost and Usage Report|CUR]] + [[Amazon Athena|Athena]]** (detailed line items land in [[Amazon S3|S3]]; Athena is the SQL)
- *"Identify [[Amazon EC2|EC2 instances]] that are overprovisioned and get sizing recommendations"* → **[[AWS Compute Optimizer|Compute Optimizer]]** (ML rightsizing)
- *"Get alerted about unexpected spending spikes without setting thresholds"* → **[[AWS Cost Anomaly Detection|Cost Anomaly Detection]]** (ML learns 'normal', flags weird)
- *"Understand which service caused last month's bill increase and forecast next quarter"* → **[[AWS Cost Explorer|Cost Explorer]]** (visualize history + 12-month forecast)
- *"Decide how much [[Savings Plans|Savings Plan]] commitment to purchase"* → **Cost Explorer recommendations** (based on your historical usage)

## Pocket card

| Keyword | Answer |
|---|---|
| Visualize / analyze spend, forecast | Cost Explorer |
| Alert at % of budget | AWS Budgets |
| Most detailed / line items / SQL | CUR + Athena |
| Unusual spike, ML detection | Cost Anomaly Detection |
| Rightsize EC2/EBS/Lambda | Compute Optimizer |
| Cost per team / chargeback | Cost Allocation Tags (activate first) |
| RI / Savings Plan buy advice | Cost Explorer |
| Custom internal billing views | Billing Conductor |

---
**Up:** [[Drills Map]]
