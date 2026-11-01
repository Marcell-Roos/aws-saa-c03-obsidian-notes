---
tags: [service, cat/security, scope/in]
aliases: ["policy evaluation"]
---

# IAM Policy Evaluation Logic

The source had this only as an image. The rule: **an explicit deny always wins, and everything starts denied.**

```mermaid
flowchart TD
    S["Request"] --> D{"Explicit deny in any policy?"}
    D -->|"Yes"| X["Deny"]
    D -->|"No"| O{"Allowed by SCP and RCP?"}
    O -->|"No"| X
    O -->|"Yes"| R{"Allowed by resource policy?"}
    R -->|"Yes, same account"| A["Allow"]
    R -->|"No"| I{"Allowed by identity policy?"}
    I -->|"No"| X
    I -->|"Yes"| B{"Allowed by permission boundary and session policy?"}
    B -->|"No"| X
    B -->|"Yes"| A
```

For [[Cross-Account Access|cross-account access]], **both** the identity policy in the caller's account and the resource policy must allow the action. This diagram is simplified from AWS's full flow.

## Exam tasks
- [[Task 1.1 Design secure access to AWS resources]]

---
**Up:** [[AWS IAM]] · **Map:** [[Security Identity and Compliance Map]]
