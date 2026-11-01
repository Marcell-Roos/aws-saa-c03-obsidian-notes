---
tags: [service, cat/storage, scope/in]
aliases: ["Storage Gateway", "S3 File Gateway", "Volume Gateway", "Tape Gateway", "FSx File Gateway"]
---

# AWS Storage Gateway

[[Amazon S3|S3]] is a proprietary storage technology and only way to expose S3 data on-premise is using AWS Storage Gateway.

**AWS Storage Gateway** is a bridge between on-premise data and cloud data in S3. Our hybrid storage service will allow on-premises to seamlessly use the AWS Cloud ([[Disaster Recovery Strategies|disaster recovery]], backup & restore, tiered storage).

Types of Storage Gateway:

- **S3 File Gateway** - offers file-based access to objects in Amazon S3. It allows us to store and retrieve objects in Amazon S3 using file protocols, such as **NFS and SMB**. Most recently used data is cached in the file gateway. It supports S3 Standard, [[S3 Storage Classes|Standard-IA]], One Zone-IA, Intelligent-Tiering and Glacier storage classes, but not Glacier Instant Retrieval. Moving objects to colder classes is normally done with a [[S3 Lifecycle Rules|Lifecycle Policy]].

    To access our buckets we must create [[IAM Users Groups and Roles|IAM role]] for each File Gateway. Also if we use SMB we can use its integration with Active Directory for user authentication.

- **FSx File Gateway** (no longer available to new customers) - offers native access to [[Amazon FSx]] for Windows File Server. It has local cache for frequently accessed data.

- **Volume Gateway** - provides [[Storage Types|block storage]] to on-premises applications using iSCSI protocol, with data asynchronously backed up to AWS.

    There are two modes for Volume Gateway:

    - **Cached Volumes** - frequently accessed data is cached locally, while the primary data is stored in S3.
    - **Stored Volumes** - entire datasets are stored locally, with scheduled backups to S3.

- **Tape Gateway** - enables us to use Amazon S3 and Glacier as a scalable, cost-effective solution for archival and backup data stored on physical tapes. It presents a virtual tape library (VTL) interface, compatible with leading backup software.

Using Storage Gateway means we need on-premises virtualization. Otherwise, we can use a Storage Gateway Hardware Appliance. It has the required CPU, memory, network and SSD cache resources.

## Exam tasks
- [[Task 3.1 Determine high-performing and or or scalable storage solutions]]
- [[Task 3.5 Determine high-performing data ingestion and transformation solutions]]
- [[Task 4.1 Design cost-optimized storage solutions]]

---
**Map:** [[Storage Map]]
