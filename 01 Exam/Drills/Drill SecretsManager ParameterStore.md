---
tags: [drill, scope/in]
---

# Drill SecretsManager ParameterStore

Adapted from [RonitSachdev/aws-saa-c03-guides](https://github.com/RonitSachdev/aws-saa-c03-guides) (CC BY 4.0), with outdated facts changed.

## Question patterns

- *"Automatically rotate the [[Amazon RDS|RDS]] database password every 30 days."* → **[[AWS Secrets Manager|Secrets Manager]]** (native RDS rotation via built-in [[AWS Lambda|Lambda]]).
- *"Store application configuration values at the lowest possible cost."* → **[[SSM Parameter Store|Parameter Store]] standard tier** (free).
- *"Organize config per environment like /prod/db/url and /dev/db/url, with [[AWS IAM|IAM]] scoped per environment."* → **Parameter Store hierarchical paths**.
- *"Share a database secret with an application in another AWS account."* → **Secrets Manager cross-account resource policy**.
- *"Developers hardcoded the DB password in the code — what's the fix?"* → **Secrets Manager + [[IAM Users Groups and Roles|IAM role]], app fetches at runtime** (never in code/env files).
- *"Store an encrypted license key for free."* → **Parameter Store SecureString** (KMS-encrypted, still free).
- *"Rotate credentials without application downtime."* → **Secrets Manager** — app fetches the current secret at connection time.
- *"Secret is 20KB of JSON credentials."* → **Secrets Manager** (64KB limit; Parameter Store caps at 4/8KB).
- *"Audit who accessed the database secret."* → **Either service + [[AWS CloudTrail|CloudTrail]]** (all API access is logged).

## Pocket card

| Keyword | Answer |
|---|---|
| "Automatic rotation" (any phrasing) | Secrets Manager |
| RDS/Redshift/DocumentDB creds | Secrets Manager (built-in rotation Lambda) |
| Cheapest / free config store | Parameter Store standard |
| Hierarchical paths /prod/... | Parameter Store |
| Cross-account secret sharing | Secrets Manager |
| Encrypted param, free | Parameter Store SecureString |
| > 8KB secret | Secrets Manager (64KB) |
| Hardcoded password fix | Secrets Manager + IAM role runtime fetch |
| Rotation without downtime | Secrets Manager |
| $0.40/secret/month | Secrets Manager |

---
**Up:** [[Drills Map]]
