---
tags: [concept, scope/in]
aliases: ["federated access", "identity federation"]
---

# Federation

Federation lets users from an external identity provider access AWS without [[IAM Users Groups and Roles|IAM users]].

- **Workforce:** [[AWS IAM Identity Center]] with SAML 2.0 or an external IdP such as Microsoft Entra ID or Okta.
- **Customers of an app:** [[Amazon Cognito]] with social or OIDC sign-in.
- **Direct SAML or OIDC to [[AWS IAM|IAM]]:** IAM identity providers with a role assumed through [[AWS STS]].
- **On-premises Active Directory:** connect it through [[AWS Directory Service]].

## Exam tasks
- [[Task 1.1 Design secure access to AWS resources]]

---
**Up:** [[AWS IAM]]
