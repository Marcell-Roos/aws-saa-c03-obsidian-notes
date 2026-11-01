---
tags: [service, cat/management, scope/in]
aliases: ["Control Tower"]
---

# AWS Control Tower

**AWS Control Tower** is a service that provides a way to set up and govern a secure, multi-account AWS environment based on AWS best practices. It is designed for organizations that need to manage multiple AWS accounts and provides a pre-configured environment called a landing zone. The landing zone includes baseline [[AWS IAM|IAM]] roles, account structures, and network configurations.

Benefits:

- Automate the set up of our environment.
- Automate ongoing policy management using controls.
- Detect policy violations and remediate them.
- Monitor compliance through an interactive dashboard.

**Control Tower Controls** (formerly guardrails)

It provides ongoing governance for our Control Tower environment (AWS Accounts).

- **Preventive control** - using [[Service Control Policies|SCPs]] (e.g. **restrict regions across all our accounts**).
- **Detective control** - using [[AWS Config]] (e.g. **identify untagged resources**).

**Proactive controls** act at the time of deployment (using [[AWS CloudFormation|CloudFormation]] Hooks), ensuring that resources are compliant with the organization's security policies before they are launched.

## Exam tasks
- [[Task 1.1 Design secure access to AWS resources]]

---
**Up:** [[AWS Organizations]] · **Map:** [[Management and Governance Map]]
