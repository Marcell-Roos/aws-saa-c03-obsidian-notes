---
tags: [drill, scope/in]
---

# Drill Cognito

Adapted from [RonitSachdev/aws-saa-c03-guides](https://github.com/RonitSachdev/aws-saa-c03-guides) (CC BY 4.0), with outdated facts changed.

## Question patterns

- *"Mobile app needs user sign-up, sign-in, and login with Google and Facebook"* → **[[Amazon Cognito|Cognito User Pools]]** (directory + social login + hosted UI).
- *"Authenticated app users must upload files directly to [[Amazon S3|S3]] from the device"* → **Cognito Identity Pools** (JWT → [[AWS STS|STS]] → temporary AWS credentials; only creds can call S3).
- *"Allow users to browse limited content without creating an account"* → **Identity Pool unauthenticated (guest) access**.
- *"Authenticate users of a REST API on [[Amazon API Gateway|API Gateway]] without custom code"* → **Cognito User Pool authorizer** (API Gateway validates the JWT for you).
- *"Each user may only read and write objects in their own S3 prefix"* → **Identity Pool + [[IAM Policy Structure|IAM policy]] variables** (`${cognito-identity...:sub}` scopes one policy per user).
- *"Company employees need SSO access to multiple AWS accounts"* → **[[AWS IAM Identity Center|IAM Identity Center]], NOT Cognito** (workforce = Identity Center; customers = Cognito).
- *"Enterprise customers must log into your SaaS app with their corporate SAML identity provider"* → **User Pools with SAML federation** (still authentication — still the login box).
- *"Add [[IAM Password Policy and MFA|MFA]] to your application's customer logins"* → **User Pools** (MFA lives where authentication lives).

## Pocket card

| Keyword | Answer |
|---|---|
| Sign-up / sign-in / user directory | User Pools |
| JWT tokens | User Pools |
| Social login (Google/Facebook/Apple), SAML | User Pools (federation) |
| Hosted UI, MFA | User Pools |
| API Gateway / [[Application Load Balancer\|ALB]] authorizer | User Pool authorizer |
| Temporary AWS credentials for app users | Identity Pools (via STS) |
| Direct app access to S3/DynamoDB | Identity Pools |
| Guest / unauthenticated access | Identity Pools |
| Each user only their own folder | Identity Pool + IAM policy variables |
| Employees SSO to AWS accounts | IAM Identity Center (never Cognito) |
| Memory hook | User Pool = login box (JWT); Identity Pool = exchange desk (creds) |

---
**Up:** [[Drills Map]]
