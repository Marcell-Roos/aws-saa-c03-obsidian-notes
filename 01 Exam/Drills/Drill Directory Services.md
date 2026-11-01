---
tags: [drill, scope/in]
---

# Drill Directory Services

Adapted from [RonitSachdev/aws-saa-c03-guides](https://github.com/RonitSachdev/aws-saa-c03-guides) (CC BY 4.0), with outdated facts changed.

## Question patterns

- *"Deploy [[FSx for Windows File Server]]; users must authenticate with existing on-prem AD identities"* → **[[AWS Directory Service|Managed Microsoft AD]] with a trust, or AD Connector** (both let on-prem identities work; pick whichever the options offer).
- *"Security policy requires that no user identities are stored in the cloud"* → **AD Connector** (proxy only — all auth redirected on-prem, nothing stored in AWS).
- *"Small company needs a low-cost, basic LDAP-compatible directory for one application"* → **Simple AD** (cheap Samba standalone, now closed to new customers).
- *"[[Amazon EC2|EC2]] Windows instances must join a domain, and [[IAM Password Policy and MFA|MFA]] is required"* → **AWS Managed Microsoft AD** (real AD: domain join + MFA; Simple AD has neither MFA nor trust).
- *"Establish a two-way trust between AWS and the on-premises domain so users on both sides access resources"* → **Managed Microsoft AD** (the only option supporting trust relationships).
- *"[[Amazon RDS|RDS]] for SQL Server with Windows Authentication for corporate users"* → **Managed Microsoft AD** (RDS integrates with it directly; add a trust for on-prem users).
- *"WorkSpaces desktops authenticating against on-prem AD without replicating the directory"* → **AD Connector** (phone line: auth flows back on-prem).

## Pocket card

| Keyword | Answer |
|---|---|
| Full AD features in AWS | Managed Microsoft AD |
| Trust relationship with on-prem | Managed Microsoft AD (two-way trust) |
| MFA + domain join | Managed Microsoft AD |
| No identities stored in cloud | AD Connector |
| Proxy / redirect auth to on-prem | AD Connector |
| Low cost, basic LDAP, small org | Simple AD |
| No trust, no MFA | Simple AD's limits |
| [[Amazon FSx\|FSx]] Windows / WorkSpaces / RDS SQL Server | All need a directory — pick from the three |
| Memory hook | Full copy w/ trust / phone line / budget clone |

---
**Up:** [[Drills Map]]
