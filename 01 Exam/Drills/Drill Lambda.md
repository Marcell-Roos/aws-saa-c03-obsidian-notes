---
tags: [drill, scope/in]
---

# Drill Lambda

Adapted from [RonitSachdev/aws-saa-c03-guides](https://github.com/RonitSachdev/aws-saa-c03-guides) (CC BY 4.0), with outdated facts changed.

## Question patterns

- *"90-minute video transcoding job — can it run on [[AWS Lambda|Lambda]]?"* → **No — [[AWS Batch]] / [[AWS Fargate|Fargate]]** (15-minute hard limit; [[AWS Step Functions|Step Functions]] only if divisible into <15-min steps)
- *"Generate a thumbnail whenever an image lands in [[Amazon S3|S3]]"* → **S3 event notification → Lambda** (the canonical async trigger)
- *"API is fast normally but has latency spikes after idle periods"* → **[[Lambda Concurrency|Provisioned Concurrency]]** (Pre-warmed = no cold starts)
- *"Lambda scaling overwhelms a legacy database that handles only 50 connections"* → **Reserved Concurrency** cap (Restricted) — and mention **[[RDS Proxy]]**
- *"Lambda must query an [[Amazon RDS|RDS]] database in a private [[Amazon VPC|subnet]]"* → **attach Lambda to the VPC + RDS Proxy** (add NAT if it still needs internet)
- *"CPU-intensive function is too slow"* → **increase memory** (CPU scales with memory — the counterintuitive one)
- *"Run a cleanup script every night at 2 AM, no servers"* → **[[Amazon EventBridge|EventBridge]] schedule → Lambda** (serverless cron)
- *"Validate JWT tokens / call an external auth service at the edge"* → **[[CloudFront Functions and Lambda@Edge|Lambda@Edge]]** (network calls allowed; CF Functions can't)
- *"Rewrite URLs or add security headers on millions of requests, cheapest"* → **CloudFront Functions** (sub-ms, ~1/6 price, no network)
- *"Asynchronously invoked function fails and events disappear"* → **DLQ / on-failure destination** (async retries twice, then drops)
- *"Lambda should process [[Amazon SQS|SQS]] messages"* → **Event Source Mapping** (Lambda pulls in batches; failures return to the queue)

## Pocket card

| Keyword | Answer |
|---|---|
| Job > 15 minutes | NOT Lambda → Batch / Fargate |
| Divisible into <15-min steps | Step Functions |
| CPU-bound slow function | Increase memory |
| Cold start latency | Provisioned Concurrency (Pre-warmed) |
| Protect downstream / cap invocations | Reserved Concurrency (Restricted) |
| Lambda + RDS | RDS Proxy (+ VPC config) |
| VPC Lambda lost internet | [[NAT Gateways\|NAT Gateway]] / VPC endpoints |
| Async failures lost | DLQ / failure destination |
| SQS / [[Amazon Kinesis\|Kinesis]] / DDB Streams | Event Source Mapping (pull, batches) |
| S3 / SNS / EventBridge | Async push (2 retries) |
| Serverless cron | EventBridge schedule → Lambda |
| Shared dependencies | Layers |
| Deps > 250 MB | Container image (10 GB) |
| Function permissions | Execution role |
| Edge + network calls / JWT | Lambda@Edge |
| Edge header/URL tweak, cheapest | CloudFront Functions |
| Max runtime / memory / concurrency | 15 min / 10 GB / 1,000 default |

---
**Up:** [[Drills Map]]
