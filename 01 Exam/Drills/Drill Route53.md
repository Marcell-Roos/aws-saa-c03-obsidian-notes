---
tags: [drill, scope/in]
---

# Drill Route53

Adapted from [RonitSachdev/aws-saa-c03-guides](https://github.com/RonitSachdev/aws-saa-c03-guides) (CC BY 4.0), with outdated facts changed.

## Question patterns

- *"Point the apex/root domain example.com at an [[Application Load Balancer]]"* → **[[CNAME vs Alias Records|Alias record]]** (CNAME is forbidden at the apex; Alias is the AWS answer, free and auto-tracking).
- *"Active-passive setup: send traffic to the standby region only when the primary fails"* → **Failover [[Route 53 Routing Policies|routing policy]] + health check** ("active-passive" is the giveaway).
- *"Test a new app version by sending 10% of users to it"* → **Weighted routing** (canary = percentages = weights).
- *"Users in Germany must see the German-language site"* → **[[Route 53 Geolocation Routing|Geolocation]]** (user's location is a RULE, not a performance choice — and don't forget the Default record).
- *"Serve global users with the best possible performance"* → **Latency routing** ("fastest" = latency).
- *"Gradually increase the share of traffic going to the new region"* → **[[Route 53 Geoproximity Routing|Geoproximity]] with bias** ("shift traffic share" / "bias" is Geoproximity's name tag).
- *"Health-check an endpoint that has a private IP inside a [[Amazon VPC|VPC]]"* → **[[Amazon CloudWatch|CloudWatch]] alarm-based health check** (global checkers can't see inside your VPC).
- *"Return several healthy IPs and let clients pick, without a [[Elastic Load Balancing|load balancer]]"* → **Multi-Value answer routing** (up to 8 healthy records).
- *"Multi-region app needs near-INSTANT failover; [[DNS Fundamentals|DNS]] caching delays are unacceptable"* → **[[AWS Global Accelerator|Global Accelerator]] instead of [[Amazon Route 53|Route 53]]** (anything in the request path beats a phonebook when clients cache old answers).

## Pocket card

| Keyword in question | Answer |
|---|---|
| Root/apex domain → ALB/CloudFront/S3 | **Alias record** |
| name → name, NOT at apex | CNAME |
| "A/B test", "10% canary" | **Weighted** |
| "best performance", "lowest latency" | **Latency** |
| "active-passive", "DR site" | **Failover** + health check |
| "users in country X get X content", compliance | **Geolocation** (+ Default record) |
| "bias", "shift traffic share between regions" | **Geoproximity** |
| up to 8 healthy answers, DNS-level LB | **Multi-Value** |
| DNS only inside a VPC | **Private hosted zone** |
| health check a private endpoint | **CloudWatch alarm-based check** |
| combine many health checks | Calculated health check |
| instant multi-region failover, no DNS lag | **Global Accelerator** |

---
**Up:** [[Drills Map]]
