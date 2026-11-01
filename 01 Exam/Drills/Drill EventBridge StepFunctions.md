---
tags: [drill, scope/in]
---

# Drill EventBridge StepFunctions

Adapted from [RonitSachdev/aws-saa-c03-guides](https://github.com/RonitSachdev/aws-saa-c03-guides) (CC BY 4.0), with outdated facts changed.

## Question patterns

- *"Run a cleanup [[AWS Lambda|Lambda]] every night at 2 AM without managing servers."* → **[[Amazon EventBridge|EventBridge]] scheduled rule → Lambda** (serverless cron, no [[Amazon EC2|EC2]] crontab).
- *"Ingest events from Zendesk/Datadog into AWS and route them to Lambda."* → **EventBridge partner event bus** (SaaS integration is EventBridge's exclusive turf).
- *"Order workflow needs retries, error handling, and a manual approval step that may take days."* → **[[AWS Step Functions|Step Functions]] Standard** (up to 1 year + human-in-the-loop).
- *"Multi-step data pipeline of Lambdas exceeds 15 minutes end to end."* → **Step Functions** (orchestrate, don't chain — Lambda's 15-min cap is per function, the workflow can run far longer).
- *"Process each item in an array of records as a separate step."* → **Map state** (built-in for-each).
- *"Need an audit trail showing the input/output of every step of each execution."* → **Step Functions Standard** execution history.
- *"Route only events where a specific JSON field matches a value, to different targets."* → **EventBridge rule with content-based filtering**.
- *"Millions of short-lived, high-frequency workflow executions at lowest cost."* → **Step Functions Express**.
- *"Reprocess last week's events after fixing a bug."* → **EventBridge archive + replay**.
- *"Retry a failing step with exponential backoff, no custom retry code."* → **Step Functions Retry** (built into the state definition).

## Pocket card

| Keyword | Answer |
|---|---|
| Serverless cron / "nightly job" | EventBridge scheduled rule |
| SaaS events (Zendesk, Datadog) | EventBridge partner event bus |
| Content-based event filtering | EventBridge rule |
| Replay past events | EventBridge archive + replay |
| Cross-account event routing | EventBridge cross-account bus |
| Huge [[SNS and SQS Fan-Out\|fan-out]] push / SMS / mobile | [[Amazon SNS\|SNS]] (not EventBridge) |
| Multi-step workflow, retries, audit | Step Functions |
| Workflow > 15 min | Step Functions (not Lambda chain) |
| Human approval / up to 1 year | Standard workflow |
| High-volume short IoT / < 5 min | Express workflow |
| For-each over items | Map state |
| Branching logic | Choice state |
| Backoff retries, no code | Built-in Retry |

---
**Up:** [[Drills Map]]
