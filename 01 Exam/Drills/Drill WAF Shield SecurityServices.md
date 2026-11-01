---
tags: [drill, scope/in]
---

# Drill WAF Shield SecurityServices

Adapted from [RonitSachdev/aws-saa-c03-guides](https://github.com/RonitSachdev/aws-saa-c03-guides) (CC BY 4.0), with outdated facts changed.

## Question patterns

- *"Block SQL injection attacks against an application behind an [[Application Load Balancer|ALB]]"* → **[[AWS WAF|WAF]] on the ALB** (L7 rules read HTTP).
- *"Limit each client IP to 2,000 requests per 5 minutes"* → **WAF rate-based rule** ("per IP rate limit" is WAF's signature move).
- *"Protection against common DDoS attacks at no additional cost"* → **[[AWS Shield|Shield Standard]]** (free, automatic, L3/L4).
- *"Company suffered a large DDoS, wants expert support during attacks and refunds for attack-related scaling costs"* → **Shield Advanced** (DRT + cost protection = the $3k tier).
- *"Ensure WAF rules are applied to all ALBs across 50 accounts, including future accounts"* → **[[AWS Firewall Manager|Firewall Manager]]** (org-wide auto-apply; needs [[AWS Organizations|Organizations]] + Config).
- *"Identify [[Amazon S3|S3 buckets]] containing personally identifiable information"* → **[[Amazon Macie|Macie]]** (PII in S3, full stop).
- *"Alert when [[Amazon EC2|EC2 instances]] are used for cryptocurrency mining or credentials are compromised"* → **[[Amazon GuardDuty|GuardDuty]]** (ML on [[AWS CloudTrail|CloudTrail]]/Flow/DNS logs, agentless).
- *"Continuously scan EC2 instances and container images for software vulnerabilities (CVEs)"* → **Inspector** ([[AWS Systems Manager|SSM]] agent on EC2, [[Amazon ECR|ECR]], [[AWS Lambda|Lambda]]).
- *"Single pane of glass for security findings across all accounts and services"* → **[[AWS Security Hub|Security Hub]]** (the aggregation dashboard).
- *"After a GuardDuty finding, analyze and identify the root cause of the incident"* → **Detective** (post-finding investigation graph).
- *"Auditor requests AWS's SOC 2 / PCI compliance reports"* → **Artifact** (self-service report downloads).

## Pocket card

| Keyword | Answer |
|---|---|
| SQLi / XSS / HTTP filtering | WAF |
| Rate limit per IP | WAF rate-based rule |
| Test rule without blocking | WAF Count mode |
| WAF attach points | CloudFront, ALB, API GW, AppSync, Cognito (never NLB/EC2) |
| Free automatic DDoS (L3/L4) | Shield Standard |
| L7 DDoS / DRT / cost protection | Shield Advanced ($3k/mo) |
| Security policies across org, auto for new accounts | Firewall Manager (needs Organizations + Config) |
| Inspect ALL VPC traffic L3–L7 | Network Firewall |
| Cryptomining / odd API calls / no agents | GuardDuty |
| PII in S3 | Macie |
| CVEs on EC2/ECR/Lambda | Inspector |
| One findings dashboard + compliance checks | Security Hub |
| Root cause after a finding | Detective |
| SOC/PCI/ISO reports for auditors | Artifact |

---
**Up:** [[Drills Map]]
