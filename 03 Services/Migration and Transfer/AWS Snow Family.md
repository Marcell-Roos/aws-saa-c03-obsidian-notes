---
tags: [service, cat/migration, scope/in]
aliases: ["Snow Family", "Snowball", "Snowball Edge", "Snowcone", "Snowmobile"]
---

# AWS Snow Family

> [!warning] Mostly closed
> See the status table below. It stays on the exam's in-scope list.

Physical devices that move data to AWS and run compute at disconnected sites. The exam guide still lists this family, but availability has changed a lot.

| Device | Status |
| --- | --- |
| Snowball Edge Storage Optimized 210 TB | No new customers since 7 October 2025 |
| Snowball Edge Compute Optimized | No new customers since 7 October 2025 |
| Snowball Edge 80 TB and GPU models | Shut down 12 November 2025 |
| Snowcone | Not in the current Snow docs, so treat it as gone |
| Snowmobile | Shut down 14 March 2024 |

New customers are directed to [[AWS DataSync]] online, AWS Data Transfer Terminal for physical transfers, and [[AWS Outposts]] for edge compute.

**For the exam:** if moving data over the network would take more than about a week, Snow is the classic answer. Snowball can't import directly into Glacier: data lands in [[Amazon S3|S3]], then a [[S3 Lifecycle Rules|lifecycle rule]] moves it.

---
**Map:** [[Migration and Transfer Map]]
