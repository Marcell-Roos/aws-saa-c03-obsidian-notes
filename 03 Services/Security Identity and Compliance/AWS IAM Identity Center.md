---
tags: [service, cat/security, scope/in]
aliases: ["IAM Identity Center", "AWS SSO"]
---

# AWS IAM Identity Center

**AWS IAM Identity Center** (formerly AWS SSO) is a cloud-based service that simplifies managing access to multiple AWS accounts in [[AWS Organizations]] and business applications.

An **Identity Provider** is a service that manages and verifies identities of users within an organization. It authenticates users and provides identity tokens that can be used to grant access to applications and services. IdPs often use standard protocols like SAML 2.0, OpenID Connect.

**IAM Identity Center Permissions & Assignments**

- **Multi-Account Permissions** - used to manage access across AWS accounts in our AWS Organization. We can create permission sets (collection of one or more [[IAM Policy Structure|IAM policies]] assigned to users and groups to define AWS access).

- **Application Assignments** - used for SSO access to many SAML 2.0 business applications. It provides required URLs, certificates and metadata.
- **Attribute-Based Access Control (ABAC)** - fine-grained permissions based on users’ attributes stored in IAM Identity Center Identity Store. Used to define permissions once, then modify AWS access by changing the attributes.

## Exam tasks
- [[Task 1.1 Design secure access to AWS resources]]

---
**Up:** [[AWS IAM]] · **Map:** [[Security Identity and Compliance Map]]
