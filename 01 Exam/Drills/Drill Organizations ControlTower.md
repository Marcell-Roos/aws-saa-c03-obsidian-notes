---
tags: [drill, scope/in]
---

# Drill Organizations ControlTower

Adapted from [RonitSachdev/aws-saa-c03-guides](https://github.com/RonitSachdev/aws-saa-c03-guides) (CC BY 4.0), with outdated facts changed.

## Question patterns

- *"Prevent all accounts in the organization from launching resources outside approved regions"* → **[[Service Control Policies|SCP]] on the root/OU** (org-wide ceiling = SCP)
- *"An SCP denies an action, yet the management account can still perform it — why?"* → **SCPs don't apply to the management account** (the exemption trap)
- *"New teams need AWS accounts that come pre-configured with security baselines, via self-service"* → **[[AWS Control Tower|Control Tower]] Account Factory** (standardized account vending)
- *"Company wants a single bill and to share [[EC2 Reserved Instances|Reserved Instance]] discounts across accounts"* → **[[AWS Organizations|Organizations]] consolidated billing** (pooled usage, shared RI/SP)
- *"Multiple accounts must use the same [[Amazon VPC|VPC]] subnets / a central [[AWS Transit Gateway|Transit Gateway]]"* → **[[AWS Resource Access Manager|AWS RAM]]** (share, don't duplicate)
- *"[[AWS IAM|IAM]] user has full admin policy in a member account but is denied — what to check?"* → **The SCP** (ceiling overrides IAM allow)
- *"Automatically set up a multi-account environment following AWS best practices"* → **Control Tower** (landing zone + guardrails)
- *"Guardrail that flags noncompliant resources but doesn't block creation"* → **Detective guardrail** (Config rule; preventive = SCP = block)

## Pocket card

| Keyword | Answer |
|---|---|
| Block actions org-wide / by OU | SCP |
| SCP grants permissions? | Never — ceiling only (needs IAM allow too) |
| SCP vs management account | Doesn't apply — exempt |
| One bill, shared RI/SP discounts | Consolidated billing |
| Automated governed multi-account setup | Control Tower |
| Self-service standardized new accounts | Account Factory |
| Preventive guardrail | SCP (blocks) |
| Detective guardrail | Config rule (flags) |
| Share subnets / TGW / resolver rules | RAM |
| Admin denied in member account | Check the SCP |

---
**Up:** [[Drills Map]]
