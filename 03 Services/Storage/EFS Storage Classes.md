---
tags: [service, cat/storage, scope/in]
---

# EFS Storage Classes

**Storage Classes**

- **Standard** - for frequently accessed files. Data is redundantly stored across multiple [[AWS Global Infrastructure|Availability Zones]] within an AWS Region.
- **Infrequent Access (IA)** - for files that are accessed less frequently but require the same durability and availability as the [[Amazon EFS|EFS]] Standard class. It has lower price to store, but has retrieval fee.
- **Archive** - for rarely accessed data (few times each year). It is 50% cheaper.

We need to implement lifecycle policies to move files between storage tiers.

## Exam tasks
- [[Task 4.1 Design cost-optimized storage solutions]]

---
**Up:** [[Amazon EFS]] · **Map:** [[Storage Map]]
