---
tags: [drill, scope/in]
---

# Drill CloudWatch CloudTrail Config

Adapted from [RonitSachdev/aws-saa-c03-guides](https://github.com/RonitSachdev/aws-saa-c03-guides) (CC BY 4.0), with outdated facts changed.

## Question patterns

- *"Determine who terminated a production [[Amazon EC2|EC2 instance]] last week."* → **[[AWS CloudTrail|CloudTrail]]** (API audit = who did what).
- *"Alert when application memory usage exceeds 80% on EC2."* → **[[Amazon CloudWatch|CloudWatch]] agent + custom metric + alarm** (memory is not a default metric).
- *"Trigger an alarm when the app logs more than 100 ERROR lines in 5 minutes."* → **Metric filter on [[CloudWatch Logs]] + alarm**.
- *"Show the configuration of a [[Security Groups|security group]] as of last Tuesday, and flag any SG allowing SSH from the internet."* → **[[AWS Config]]** (timeline + managed rule).
- *"Automatically fix noncompliant security groups without manual work."* → **Config rule + [[SSM Automation]] remediation**.
- *"A request spans 10 microservices; find which one is slow."* → **[[AWS X-Ray|X-Ray]]** (distributed tracing).
- *"Process log entries in real time as they are written."* → **CloudWatch Logs subscription filter → [[Amazon Kinesis|Kinesis]]/Lambda**.
- *"Identify who downloaded a specific [[Amazon S3|S3]] object."* → **CloudTrail data events** (object-level = opt-in, extra cost).
- *"Keep API activity records for 7 years, tamper-evident."* → **Trail → S3 + log file integrity validation** (free history is only 90 days).
- *"Prevent anyone in the org from disabling CloudTrail."* → **[[Service Control Policies|SCP]]** (Config detects; SCP prevents).

## Pocket card

| Keyword | Answer |
|---|---|
| Performance, health, alarms | CloudWatch |
| Who did what / API audit | CloudTrail |
| Config history / compliance | AWS Config |
| EC2 memory or disk-space metric | CloudWatch agent (not default) |
| Count log pattern → alarm | Metric filter |
| Query logs interactively | Logs Insights |
| Real-time log streaming | Subscription filter → Kinesis/Lambda |
| Too many alarms / noise | Composite alarm |
| S3 object-level "who" | CloudTrail data events (opt-in) |
| Logs beyond 90 days | Trail → S3, multi-region |
| Tamper-proof logs | Log file integrity validation |
| Unusual API spike | CloudTrail Insights |
| Auto-fix noncompliance | Config + [[AWS Systems Manager\|SSM]] remediation |
| PREVENT actions | SCP (never Config) |
| Trace across microservices | X-Ray |

---
**Up:** [[Drills Map]]
