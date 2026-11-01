---
tags: [drill, scope/in]
---

# Drill IAM

Adapted from [RonitSachdev/aws-saa-c03-guides](https://github.com/RonitSachdev/aws-saa-c03-guides) (CC BY 4.0), with outdated facts changed.

## Question patterns

- *"An application on [[Amazon EC2|EC2]] needs to write to [[Amazon DynamoDB|DynamoDB]]. What's the MOST secure way to provide credentials?"* → **[[IAM Users Groups and Roles|IAM role]] attached to the instance (instance profile)** — never [[AWS Access Methods|access keys]] on the box.
- *"A [[AWS Lambda|Lambda function]] must read from an [[Amazon S3|S3 bucket]]. How should it authenticate?"* → **Lambda execution role** with S3 read permissions — same costume pattern, serverless flavor.
- *"Users in Account A need temporary access to resources in Account B."* → **Create a role in Account B with a trust policy trusting Account A; users [[AWS STS|AssumeRole]] via STS** — "temporary" + "another account" = cross-account role.
- *"A user's identity policy allows s3:PutObject, but uploads fail with Access Denied."* → **Look for an explicit Deny — [[S3 Access Control|bucket policy]], [[Service Control Policies|SCP]], or [[IAM Permission Boundaries|permission boundary]]** — explicit Deny always beats Allow.
- *"An action works in a standalone account but fails in an account inside [[AWS Organizations]]."* → **A Service Control Policy is blocking it** — "Organizations" is the tell.
- *"Developers may create [[AWS IAM|IAM]] roles for their apps, but security wants a guarantee those roles can never exceed a defined permission set."* → **Permission boundaries** — "maximum permissions" / "cannot exceed" is the signal.
- *"5,000 employees with existing Active Directory logins need access to multiple AWS accounts without creating IAM users."* → **[[AWS IAM Identity Center|IAM Identity Center]] with SAML federation to AD** — "existing corporate directory" + "multiple accounts" + "no IAM users".
- *"An application needs short-lived credentials that expire automatically."* → **STS AssumeRole** — "temporary/short-lived credentials" is literally STS's product.
- *"Require that users can only terminate EC2 instances if they've signed in with [[IAM Password Policy and MFA|MFA]]."* → **Policy Condition with `aws:MultiFactorAuthPresent`** — sensitive action + MFA = that condition key.
- *"A new AWS account was just created. What should be done FIRST to secure it?"* → **Enable MFA on the root user, delete/avoid root access keys, create an admin user for daily work.**

## Pocket card

| Keyword in the question | Answer |
|---|---|
| EC2/app needs AWS access, "most secure" | Instance role (instance profile), never keys |
| Lambda needs permissions | Execution role |
| Hardcoded / stored access keys | Wrong — replace with a role |
| Temporary / short-lived credentials | STS AssumeRole |
| Access across AWS accounts | Role in target account + trust policy |
| Third party assumes your role safely | ExternalId in trust policy |
| Role exists but "can't be assumed" | Fix the trust policy |
| Allow exists but action denied | Explicit Deny / SCP / permission boundary |
| Org-wide restriction, applies even to root | SCP (AWS Organizations) |
| Cap max permissions of ONE user/role | Permission boundary |
| Policy on the resource, has a Principal | Resource-based policy (e.g., bucket policy) |
| Legacy S3 grant mechanism, avoid | S3 ACL (≠ Network ACL) |
| SSO, one login → many AWS accounts | IAM Identity Center |
| Federate Okta / Azure AD / corporate AD | IAM Identity Center + SAML 2.0 |
| Federate app customers (Google/Facebook login) | Cognito |
| Require MFA for an action | Condition: aws:MultiFactorAuthPresent |
| Root account | MFA on, no access keys, don't use daily |
| Who is my resource shared with externally? | IAM Access Analyzer |
| Find unused users / stale permissions | Credentials report / access advisor |

---
**Up:** [[Drills Map]]
