---
tags: [service, cat/security, scope/in]
aliases: ["IAM policy", "IAM policies"]
---

# IAM Policy Structure

[[AWS IAM|IAM]] Policy Components

- **Statement** - main element of an IAM policy, and it consists of one or more individual statement.
- **Sid** - identifier for the statement.
- **Effect** - specifies whether the statements allows or denies the specified action.
- **Principal (Optional)** - Specifies the entity (user, account or role) that the policy is applied to.
- **Action** - lists the specific actions that the policy allows or denies. Actions are represented as strings, often in the format "**[service]:[action]**".
- **Resource** - specifies the AWS resources.
- **Condition (Optional)** - defines conditions under which the policy statement is in effect.

## Exam tasks
- [[Task 1.1 Design secure access to AWS resources]]

---
**Up:** [[AWS IAM]] · **Map:** [[Security Identity and Compliance Map]]
