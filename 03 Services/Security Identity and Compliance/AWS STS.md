---
tags: [service, cat/security, scope/in]
aliases: ["STS", "AWS Security Token Service", "AssumeRole"]
---

# AWS STS

**AWS Security Token Service** issues temporary credentials: an access key, a secret key and a session token. They expire automatically.

- `AssumeRole`: within or across accounts
- `AssumeRoleWithSAML`: SAML federation
- `AssumeRoleWithWebIdentity`: OIDC federation
- `GetSessionToken`: MFA-protected API access

Used by [[Cross-Account Access]], [[Federation]] and every [[IAM Users Groups and Roles|IAM role]].

## Exam tasks
- [[Task 1.1 Design secure access to AWS resources]]

---
**Up:** [[AWS IAM]] · **Map:** [[Security Identity and Compliance Map]]
