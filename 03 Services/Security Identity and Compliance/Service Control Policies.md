---
tags: [service, cat/security, scope/in]
aliases: ["SCP", "SCPs"]
---

# Service Control Policies

**Service Control Policies (SCPs)** - allows us to control the services and actions that users and roles can access within the accounts of our organization (whitelist or blacklist [[AWS IAM|IAM]] actions).

Can be applied to the OU (organizational unit) or account level (does not apply to the management account). It is applied to all the users and roles of the account, including root. SCPs are inherited down the hierarchy. An SCP attached to a root or OU will affect all accounts and OUs beneath it.

It will not affect service-linked roles (service-linked roles enable other AWS services to integrate with organizations and can't be restricted).

SCPs never grant permissions; they only set the maximum available. The default `FullAWSAccess` SCP allows everything, and removing it without a replacement makes every action in member accounts fail.

## Exam tasks
- [[Task 1.1 Design secure access to AWS resources]]

---
**Up:** [[AWS Organizations]] · **Map:** [[Security Identity and Compliance Map]]
