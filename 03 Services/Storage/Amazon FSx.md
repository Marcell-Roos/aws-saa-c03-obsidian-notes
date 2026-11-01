---
tags: [service, cat/storage, scope/in]
aliases: ["FSx"]
---

# Amazon FSx

**Amazon FSx** is a fully managed service that lets us launch third party high-performance file systems on AWS.

**FSx System Deployment Options**

- **Scratch File System** - temporary storage. Data is not replicated (doesn’t persist if file server fails). It has high burst and it is used for short-term processing.
- **Persistent File System** - long-term storage. Data is replicated within same AZ. It replaces failed files within minutes. Used for long-term processing and sensitive data.

## In this topic
- [[FSx for Lustre]]
- [[FSx for NetApp ONTAP]]
- [[FSx for OpenZFS]]
- [[FSx for Windows File Server]]

## Exam tasks
- [[Task 3.1 Determine high-performing and or or scalable storage solutions]]
- [[Task 4.1 Design cost-optimized storage solutions]]

---
**Map:** [[Storage Map]]
