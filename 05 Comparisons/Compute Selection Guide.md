---
tags: [comparison, scope/in]
---

# Compute Selection Guide

```mermaid
flowchart TD
    Q{"What are you running?"}
    Q -->|"Short event code"| L["Lambda"]
    Q -->|"Containers"| C{"Manage hosts?"}
    C -->|"No"| F["Fargate"]
    C -->|"Yes"| E["ECS or EKS on EC2"]
    Q -->|"Full OS control"| EC2["EC2"]
    Q -->|"Batch jobs"| B["AWS Batch"]
    Q -->|"Big data"| M["EMR"]
    Q -->|"Web app, minimal setup"| EB["Elastic Beanstalk"]
```

## Exam tasks
- [[Task 2.1 Design scalable and loosely coupled architectures]]
- [[Task 3.2 Design high-performing and elastic compute solutions]]

---
**Up:** [[Decision Guides Map]]
