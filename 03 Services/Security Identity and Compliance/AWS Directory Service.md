---
tags: [service, cat/security, scope/in]
aliases: ["AD Connector", "Simple AD", "Managed Microsoft AD", "Directory Service"]
---

# AWS Directory Service

**AWS Directory Service** is a managed service that makes it easy to set up and run directory services in the AWS cloud or connect your AWS resources with an existing on-premises Microsoft Active Directory (AD).

**Microsoft Active Directory (AD)** is a directory service developed by Microsoft for Windows domain networks. It is a database of objects: user accounts, computers, printers, file shares, [[Security Groups|security groups]]… Objects are organized in trees and a group of trees is a forest.

AWS Directory Services

- **AWS Managed Microsoft AD** - creates our own AD in AWS, manage users locally and supports [[IAM Password Policy and MFA|MFA]]. It establishes “trust” connections with our on-premise AD. Those directories are deployed across **two AZs in a region** by default and connected to our [[Amazon VPC]].
- **AD Connector** - directory gateway (proxy) to redirect to on-premise AD, supports MFA. Users are managed on the on-premise AD.
- **Simple AD** - AD-compatible managed directory on AWS. Cannot be joined with on-premise AD.

**[[AWS IAM Identity Center|IAM Identity Center]] Active Directory Setup**

- **Connect to an AWS Managed AD** - integration is out of the box.

- **Connect to a Self-Managed AD** - we need to create two-way trust relationship using AWS Managed Microsoft AD and AD Connector.

Simple AD has been closed to new customers since 30 June 2026.

## Exam tasks
- [[Task 1.1 Design secure access to AWS resources]]

---
**Map:** [[Security Identity and Compliance Map]]
