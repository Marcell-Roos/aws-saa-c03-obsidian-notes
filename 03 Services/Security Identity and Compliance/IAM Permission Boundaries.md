---
tags: [service, cat/security, scope/in]
aliases: ["permission boundaries", "Permission Boundaries", "permission boundary"]
---

# IAM Permission Boundaries

**IAM Permission Boundaries** - advanced feature to use a managed policy to set the maximum permissions an [[AWS IAM|IAM]] entity can get. They are supported for users and roles (not groups). They can be used in combinations of [[AWS Organizations]] [[Service Control Policies|SCP]].

- Can delegate responsibilities to non administrators within their permissions boundaries.
- Allow developers to self-assign policies and manage their own permissions, while making sure they can't escalate their privileges.
- Useful to restrict one specific user (instead of a whole account using Organization & SCP).

## Exam tasks
- [[Task 1.1 Design secure access to AWS resources]]

---
**Up:** [[AWS IAM]] · **Map:** [[Security Identity and Compliance Map]]
