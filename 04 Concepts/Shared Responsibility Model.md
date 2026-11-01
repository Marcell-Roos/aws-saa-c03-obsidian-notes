---
tags: [concept, scope/in]
aliases: ["shared responsibility model"]
---

# Shared Responsibility Model

AWS secures the cloud. The customer secures what they put in it.

| AWS: security **of** the cloud | Customer: security **in** the cloud |
| --- | --- |
| Hardware, facilities, global network | Customer data and encryption choices |
| Host OS and virtualisation | [[IAM Users Groups and Roles\|IAM users]], roles and policies |
| Managed service software | Guest OS patching on [[Amazon EC2\|EC2]] |
| | Security groups, [[Network ACLs\|NACLs]] and app code |

The split moves with the service. On EC2 you patch the guest OS. On [[Amazon RDS|RDS]], AWS patches the OS and engine, while you control access and encryption. On [[AWS Lambda|Lambda]], AWS manages the runtime and you own the code and permissions.

## Exam tasks
- [[Task 1.1 Design secure access to AWS resources]]

---
**Up:** [[Concepts Map]]
