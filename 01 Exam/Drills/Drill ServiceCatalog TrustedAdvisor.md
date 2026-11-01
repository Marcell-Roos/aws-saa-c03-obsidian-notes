---
tags: [drill, scope/in]
---

# Drill ServiceCatalog TrustedAdvisor

Adapted from [RonitSachdev/aws-saa-c03-guides](https://github.com/RonitSachdev/aws-saa-c03-guides) (CC BY 4.0), with outdated facts changed.

## Question patterns

- *"Non-technical teams must deploy infrastructure, but only pre-approved configurations, without granting them broad [[AWS IAM|IAM]] permissions"* → **[[AWS Service Catalog|Service Catalog]]** (vending machine: products in portfolios, launch-on-behalf)
- *"Identify idle instances and unattached Elastic IPs to reduce the bill"* → **[[AWS Trusted Advisor|Trusted Advisor]]** (Cost Optimization pillar)
- *"Team can only see a few Trusted Advisor checks — why?"* → **Support plan** (full checks need Business Support+ or higher)
- *"Get warned before hitting an AWS service quota"* → **Trusted Advisor Service Limits check** (limits = its own pillar)
- *"Flag [[Security Groups|security groups]] allowing unrestricted access and missing root [[IAM Password Policy and MFA|MFA]]"* → **Trusted Advisor** (Security pillar)
- *"Central IT curates standard CloudFormation-based products for business units"* → **Service Catalog portfolios** (products live in portfolios, shared to users/accounts)

## Pocket card

| Keyword | Answer |
|---|---|
| Self-service approved stacks, minimal IAM | Service Catalog |
| Product / portfolio | Service Catalog terms (CFN template / group of products) |
| Idle / unused / unattached resources | Trusted Advisor (Cost) |
| Approaching quota warning | Trusted Advisor (Service Limits) |
| Open SGs, root MFA check | Trusted Advisor (Security) |
| Full checks locked | Business Support+ or higher |
| Five pillars | Cost, Performance, Security, Fault Tolerance, Service Limits |

---
**Up:** [[Drills Map]]
