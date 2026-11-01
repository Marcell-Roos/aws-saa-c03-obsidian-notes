---
tags: [service, cat/security, scope/in]
aliases: ["Shield Advanced", "Shield Standard"]
---

# AWS Shield

DDoS Protection on AWS:

- **AWS Shield Standard** - protects against DDoS attack for our website and applications, its free for all customers.
- **AWS Shield Advanced** - 24/7 premium DDoS protection ($3,000 per month per organization, plus data transfer fees).
- **[[Amazon CloudFront|CloudFront]] & [[Amazon Route 53|Route 53]]** - combined with AWS Shield, provides attack mitigation at the edge.

We should be ready to scale during attack - leverage [[AWS Auto Scaling]].

Shield Standard covers layers 3 and 4. Shield Advanced adds layer 7 mitigation through [[AWS WAF|WAF]], a response team, and cost protection during attacks.

## Exam tasks
- [[Task 1.2 Design secure workloads and applications]]

---
**Map:** [[Security Identity and Compliance Map]]
