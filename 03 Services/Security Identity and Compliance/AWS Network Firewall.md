---
tags: [service, cat/security, scope/in]
aliases: ["Network Firewall"]
---

# AWS Network Firewall

**AWS Network Firewall** protects our entire [[Amazon VPC|VPC]] (from layer 3 to layer 7). We can inspect traffic in any direction:

- VPC to VPC traffic
- Outbound to internet
- Inbound to internet
- To/from [[AWS Direct Connect|Direct Connect]] & [[AWS Site-to-Site VPN|Site-to-Site VPN]]

Internally, the AWS Network Firewall uses the AWS [[Gateway Load Balancer]]. Rules can be centrally managed cross-account to apply to many VPCs.

**Network Firewall Endpoint** - a virtual appliance deployed within our VPC that inspects and filters network traffic based on the firewall rules we configure. It provides the actual interface through which the firewall processes the traffic. It’s responsible for applying the policies and rules we define to **control incoming and outgoing network traffic**. We can allow, drop or alert for the traffic that matches the rules. All rule matches can be sent to [[Amazon S3|S3]], [[CloudWatch Logs]] and [[Amazon Data Firehose|KDF]].

## Exam tasks
- [[Task 1.2 Design secure workloads and applications]]

---
**Map:** [[Security Identity and Compliance Map]]
