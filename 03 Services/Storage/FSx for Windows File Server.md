---
tags: [service, cat/storage, scope/in]
aliases: ["FSx for Windows"]
---

# FSx for Windows File Server

**FSx for Windows File Server** - supports SMB and NTFS protocols. It can be mounted on Linux [[Amazon EC2|EC2 instances]]. We can integrate it with Microsoft AD, ACLs and user quotas. It supports Microsoft’s Distributed File System (DFS) Namespaces.

We can choose SSD or HDD for storage options. FSx for Windows can be accessed from our on-premises infrastructure (VPN or [[AWS Direct Connect|DX]]). Can be configured to be Multi-AZ and all data is backed-up daily to [[Amazon S3|S3]].

FSx for Windows File Server **can be joined to an existing on-premises Active Directory**. This allows the file system to continue using the same AD groups and policies to restrict access to the shares, folders, and files, just as it did on-premises.

---
**Up:** [[Amazon FSx]] · **Map:** [[Storage Map]]
