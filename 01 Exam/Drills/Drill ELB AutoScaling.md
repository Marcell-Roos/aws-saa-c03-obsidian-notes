---
tags: [drill, scope/in]
---

# Drill ELB AutoScaling

Adapted from [RonitSachdev/aws-saa-c03-guides](https://github.com/RonitSachdev/aws-saa-c03-guides) (CC BY 4.0), with outdated facts changed.

## Question patterns

- *"Route `/api/*` to one set of servers and `/images/*` to another"* → **[[Application Load Balancer|ALB]] path-based routing** (only L7 sees URLs)
- *"UDP-based multiplayer game needs low latency and a static IP"* → **[[Network Load Balancer|NLB]]** (ALB can't do UDP or static IPs)
- *"Inspect all traffic with a third-party firewall/IDS appliance fleet"* → **[[Gateway Load Balancer]]** (GENEVE 6081, bump-in-the-wire)
- *"LB marks instances unhealthy, but [[Amazon EC2 Auto Scaling|ASG]] doesn't replace them"* → **enable [[Elastic Load Balancing|ELB]] health checks on the ASG** (default is [[Amazon EC2|EC2]] status checks only)
- *"Payroll traffic spikes every month-end at a known time"* → **Scheduled scaling** (predictable = scheduled)
- *"Keep average CPU at 40% with minimal configuration"* → **[[ASG Scaling Policies|Target Tracking]]** ("keep metric at value" + "simplest")
- *"Serve many HTTPS domains with different certificates on one ALB"* → **[[ELB SSL Certificates and SNI|SNI]]** (multiple TLS certs, one listener)
- *"Corporate clients must whitelist fixed IP addresses for your load balancer"* → **NLB with Elastic IPs** (or [[AWS Global Accelerator|Global Accelerator]] in front of an ALB)
- *"App behind ALB needs the original client IP"* → **X-Forwarded-For header** (NLB would preserve it natively)
- *"Scale workers based on the number of unprocessed jobs"* → **ASG scaling on [[Amazon SQS|SQS]] queue depth** (backlog per instance)
- *"Millions of TCP requests per second, extreme performance"* → **NLB** ("millions" + "ultra-low latency" = L4)

## Pocket card

| Keyword | Answer |
|---|---|
| Path / host / header routing | ALB |
| HTTP, microservices, containers, [[AWS Lambda\|Lambda]] target | ALB |
| [[AWS WAF\|WAF]] on a load balancer | ALB (L7 only) |
| UDP, extreme performance, millions req/s | NLB |
| Static IP / Elastic IP / whitelisting | NLB (or Global Accelerator) |
| [[AWS PrivateLink\|PrivateLink]] endpoint service front | NLB |
| Third-party security appliances, GENEVE 6081 | GLB |
| Classic Load Balancer | Wrong answer |
| Multiple TLS certs, one LB | SNI |
| Errors during scale-in | Deregistration delay (draining) |
| Uneven traffic across AZs | Cross-zone LB (ALB free/on, NLB paid/off) |
| Client IP behind ALB | X-Forwarded-For |
| "Keep CPU at X%" simply | Target Tracking |
| Known time spikes | Scheduled scaling |
| ML-forecasted scaling | Predictive scaling |
| ASG ignores app-level failures | Enable ELB health checks on ASG |
| Scale on job backlog | SQS queue depth metric |
| Instance-level failover | ELB (in-path, instant) |
| Region-level failover | [[Amazon Route 53\|Route 53]] (DNS, slower) |

---
**Up:** [[Drills Map]]
