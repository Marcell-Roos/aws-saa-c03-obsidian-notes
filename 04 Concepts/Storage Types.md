---
tags: [concept, scope/in]
aliases: ["object storage", "block storage", "file storage"]
---

# Storage Types

| Type | How it's accessed | AWS services | Good for |
| --- | --- | --- | --- |
| **Block** | Attached volume | [[Amazon EBS]], [[EC2 Instance Store]] | Boot volumes, databases |
| **File** | NFS or SMB share | [[Amazon EFS]], [[Amazon FSx]] | Shared content, home folders |
| **Object** | HTTP API | [[Amazon S3]] | Backups, [[Data Lakes\|data lakes]], static assets |

See [[Storage Selection Guide]].

## Exam tasks
- [[Task 2.1 Design scalable and loosely coupled architectures]]
- [[Task 3.1 Determine high-performing and or or scalable storage solutions]]

---
**Up:** [[Concepts Map]]
