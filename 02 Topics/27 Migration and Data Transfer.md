---
tags: [topic, cat/migration, scope/in]
aliases: ["On-Premises Strategies", "Migration Strategies", "AWS Application Discovery Service", "AWS Application Migration Service", "MGN", "AWS DataSync", "DataSync", "AWS DMS", "DMS", "DMS Replication Details", "AWS Migration Hub", "AWS Snow Family", "Snowball", "Snow Family", "AWS Transfer Family", "Transfer Family", "AWS Transform", "AWS Storage Gateway", "Storage Gateway", "Transferring Large Datasets", "DataSync vs Storage Gateway vs Transfer Family", "Data Transfer Selection Guide", "Drill Snow Family", "Drill StorageGateway DataSync TransferFamily"]
---

# Migration and Data Transfer

> [!info] Why this matters
> "Migration and data transfer" is one of AWS's listed topic areas for this exam. Questions ask for the lowest cost or fastest way to move data, and for the right service for files, databases or whole servers.
>
> **Covers:** hybrid storage in [[Domain 3 Design High-Performing Architectures#Task 3.1|Task 3.1]], data transfer in [[Domain 3 Design High-Performing Architectures#Task 3.5|Task 3.5]], [[Domain 4 Design Cost-Optimized Architectures#Task 4.1|Task 4.1]], [[Domain 4 Design Cost-Optimized Architectures#Task 4.3|Task 4.3]].
> **Study time:** about 3 hours.

## Migration strategies

The "7 Rs" describe how to move each application.

| Strategy | Meaning | Example |
| --- | --- | --- |
| **Rehost** | Lift and shift | Application Migration Service to EC2 |
| **Relocate** | Move a hypervisor estate | VMware Cloud on AWS |
| **Replatform** | Lift, tinker and shift | Self-managed database to RDS |
| **Refactor** | Re-architect for cloud-native | Monolith to microservices |
| **Repurchase** | Move to a SaaS product | CRM to a SaaS CRM |
| **Retain** | Keep it where it is for now | Recently upgraded systems |
| **Retire** | Switch it off | Unused apps |

## Choosing a migration service

| What you are moving | Service |
| --- | --- |
| Whole servers | Application Migration Service |
| Databases | Database Migration Service |
| File shares and object data | DataSync |
| Files by SFTP, FTPS, FTP or AS2 | Transfer Family |
| Ongoing on-premises access to cloud storage | Storage Gateway |
| Huge datasets on poor connections | Snow Family, for existing customers |

## Choosing a transfer method

| Situation | Use |
| --- | --- |
| Small data, spare bandwidth | Internet or Site-to-Site VPN |
| Large, repeated transfers | Direct Connect |
| Scheduled file sync | DataSync |
| Databases | DMS |
| Global uploads to S3 | S3 Transfer Acceleration |
| Network transfer would take more than about a week | Snow Family, or physical transfer |

**Do the arithmetic.** A 1 Gbps link moves about 125 MB per second at best.

| Data | 100 Mbps | 1 Gbps | 10 Gbps |
| --- | --- | --- | --- |
| 1 TB | About 22 hours | About 2.2 hours | About 13 minutes |
| 10 TB | About 9 days | About 22 hours | About 2.2 hours |
| 100 TB | About 93 days | About 9 days | About 22 hours |

These are best-case figures. Real transfers also depend on spare capacity.

> [!example] Worked example
> 80 TB must move in two weeks, over a 100 Mbps link that is half used. At 50 Mbps it would take about 150 days. Even at full speed it would take about 74 days. A physical transfer is the only realistic option, unless a faster link can be set up in time.

For ongoing replication after the first transfer, use VPN or Direct Connect with DMS or DataSync.

## AWS DataSync

**DataSync** automates moving large amounts of data, between on-premises and AWS, and between AWS services.

- **Sources:** NFS, SMB, HDFS and object storage on-premises, and other cloud storage.
- **Destinations:** S3 (all storage classes), EFS and all FSx types.
- An **agent** is installed on-premises as a virtual machine. No agent is needed between AWS services in the same account.
- Tasks can run on a **schedule**: hourly, daily or weekly.
- It **preserves metadata and permissions** (NFS POSIX and SMB).
- It verifies data and encrypts it in transit.
- You can set a **bandwidth limit**, so that it does not swamp your link.
- A task can use up to 10 Gbps. It can run over Direct Connect, or through a VPC endpoint.

## AWS Storage Gateway

**Storage Gateway** gives on-premises applications ongoing access to cloud storage. It is the bridge for hybrid use, whereas DataSync is for moving data.

| Gateway | Protocol | Backed by | Use |
| --- | --- | --- | --- |
| **S3 File Gateway** | NFS, SMB | S3 | Files stored as objects, with a local cache of recent data |
| **FSx File Gateway** | SMB | FSx for Windows | Low-latency local cache. Closed to new customers |
| **Volume Gateway, cached** | iSCSI | S3, with EBS snapshots | Primary data in AWS, frequently used data cached locally |
| **Volume Gateway, stored** | iSCSI | Local, with backups to AWS | The whole dataset stays local, with backups to AWS |
| **Tape Gateway** | iSCSI VTL | S3 and Glacier | Replace physical tapes, and keep your backup software |

Details to remember:

- S3 File Gateway needs an IAM role for each gateway, and it can use Active Directory for SMB authentication.
- It works with S3 Standard, Standard-IA, One Zone-IA, Intelligent-Tiering and Glacier classes, but not Glacier Instant Retrieval. Lifecycle policies normally move objects to colder classes.
- A gateway runs as a virtual machine on-premises. Without virtualisation, use the hardware appliance.

| | DataSync | Storage Gateway | Transfer Family |
| --- | --- | --- | --- |
| Job | Move or sync data | Ongoing on-premises access to cloud storage | Managed SFTP, FTPS, FTP and AS2 |
| Typical use | One-off or scheduled migration | NAS replacement, tape replacement | Partners upload to S3 or EFS |

## AWS Transfer Family

**Transfer Family** provides fully managed file transfer into and out of **S3 or EFS**, using **SFTP, FTPS, FTP and AS2**.

- You pay per provisioned endpoint per hour, plus per GB.
- It can store users' credentials, or integrate with existing authentication systems.
- **AS2** exchanges EDI documents between businesses.

If partners cannot change their workflow and use SFTP, the answer is Transfer Family. Do not build an SFTP server on EC2.

## AWS Snow Family

The **Snow Family** uses physical devices to move data to AWS, and to run compute at disconnected sites.

> [!warning] Availability has changed
> Snow is still on the exam's in-scope list, but most of it has closed.

| Device | Status |
| --- | --- |
| Snowball Edge Storage Optimized 210 TB | No new customers since 7 October 2025 |
| Snowball Edge Compute Optimized | No new customers since 7 October 2025 |
| Snowball Edge 80 TB and GPU models | Shut down on 12 November 2025 |
| Snowcone | No longer in the current docs, so treat it as gone |
| Snowmobile | Shut down on 14 March 2024 |

New customers are directed to DataSync online, **AWS Data Transfer Terminal** for physical transfers, and Outposts for edge compute.

**For the exam:** if moving data over the network would take more than about a week, Snow is the classic answer. Data on a device is encrypted with KMS keys. **Snowball cannot import directly into Glacier.** Data lands in S3, then a lifecycle rule moves it. **OpsHub** is the graphical tool for managing devices.

## AWS DMS

**Database Migration Service** migrates databases to AWS quickly and securely. The **source stays available** during migration.

| Migration type | What it does |
| --- | --- |
| **Full load** | Copies existing data |
| **Full load plus CDC** | Copies, then keeps changes flowing, for minimal downtime |
| **CDC only** | Replicates ongoing changes |

**Change data capture (CDC)** reads the database's transaction log, to replicate changes continuously.

| Migration | Example | Tools |
| --- | --- | --- |
| **Homogeneous** | Oracle to RDS for Oracle | DMS, and native tools. No schema conversion |
| **Heterogeneous** | Oracle to Aurora PostgreSQL | **AWS SCT or DMS Schema Conversion**, then DMS |

Other details:

- A **replication instance** runs **replication tasks** between source and target endpoints.
- At least one endpoint must be on AWS.
- **Multi-AZ** keeps a synchronous standby replica of the replication instance.
- **DMS Serverless** handles capacity for you.
- It can also write to S3, Kinesis and other targets, so it can feed a data lake.

### Moving to Aurora

| From | To | Options |
| --- | --- | --- |
| RDS MySQL or PostgreSQL | Aurora | Restore a snapshot, or create an Aurora read replica and promote it when lag reaches 0 |
| External MySQL | Aurora MySQL | Percona XtraBackup to S3 and restore. `mysqldump` is slower |
| External PostgreSQL | Aurora PostgreSQL | Back up to S3, and import using the `aws_s3` extension |
| Both databases running | | **DMS** |

## AWS Application Migration Service

**Application Migration Service (MGN)** is AWS's main tool for rehosting, and the current AWS documentation brands it **AWS Transform MGN**. The exam guide still uses the older name.

Install the replication agent on source servers, whether physical, virtual or in another cloud. Block-level replication runs continuously to AWS. When you launch **test** or **cutover** instances, MGN converts the servers to boot natively on AWS. Cutover takes minutes.

It replaced the Server Migration Service, which shut down on 1 April 2023.

## Discovery and planning

**AWS Application Discovery Service** gathers configuration, usage and dependency data from on-premises servers, to plan a migration. It works through an agent (detailed data) or the agentless collector for VMware. It has been closed to new customers since 7 October 2025, and AWS points to AWS Transform, but it stays on the in-scope list.

**AWS Migration Hub** tracked migrations in one place. It closed to new customers on 7 November 2025.

**AWS Transform** is AWS's newer migration service.

**VM Import/Export** moves existing VMs into EC2, and back out again.

**Amazon Linux** images can run on-premises through KVM, VMware or Hyper-V.

## Exam patterns

| If the question says | Think | Why |
| --- | --- | --- |
| Replace physical tape backups, keep the backup software | Tape Gateway | Virtual tape library |
| Replace a NAS, files in S3, local access | S3 File Gateway | SMB or NFS with a cache |
| Extend capacity, primary data in the cloud | Volume Gateway, cached | |
| Keep the whole dataset local, back up to AWS | Volume Gateway, stored | |
| Migrate 50 TB from a NAS, keep permissions | DataSync | |
| Nightly sync with a bandwidth limit | DataSync | |
| Copy between S3 and EFS | DataSync | |
| Partners upload through SFTP | Transfer Family | Never SFTP on EC2 |
| Ongoing hybrid access or a one-off move | Storage Gateway or DataSync | |
| Transfer would take more than a week | Snow Family | Or Data Transfer Terminal |
| Archive to Glacier with Snowball | S3 first, then a lifecycle rule | |
| Compute at a disconnected site | Snowball Edge Compute Optimized | Existing customers |
| Migrate a database with little downtime | DMS with CDC | Source stays live |
| Oracle to PostgreSQL | SCT or DMS Schema Conversion, then DMS | Heterogeneous |
| Lift and shift servers | Application Migration Service | |
| Discover on-premises dependencies | Application Discovery Service | |
| Move VMware workloads with the same tools | VMware Cloud on AWS | |
| Migrate RDS MySQL to Aurora with little downtime | Aurora read replica, then promote | |

## Check yourself

**1.** A company wants to retire its tape library, but it must keep its existing backup software. What should it use?

- A. S3 File Gateway
- B. Tape Gateway
- C. DataSync
- D. Transfer Family

> [!success]- Answer
> **B.** Tape Gateway looks like a tape library to the backup software, while storing data in S3 and Glacier.

**2.** Partners upload files by SFTP and cannot change their process. Files must land in S3, with no servers to manage. What should be used?

- A. An SFTP server on EC2
- B. AWS Transfer Family
- C. S3 Transfer Acceleration
- D. AWS DataSync

> [!success]- Answer
> **B.** Transfer Family is a managed SFTP endpoint backed by S3.

**3.** A company must migrate 40 TB from an on-premises NAS to Amazon S3 over a 1 Gbps Direct Connect link, keeping file metadata, with minimal effort. What should it use?

- A. AWS DataSync
- B. Snowball Edge
- C. S3 File Gateway
- D. Amazon Kinesis

> [!success]- Answer
> **A.** At 1 Gbps this takes about 4 days, so the network is sufficient, and DataSync preserves metadata.

**4.** A company must move 200 TB to AWS within a month, and its 100 Mbps connection is shared. It already has a Snow relationship with AWS. What is the best option?

- A. DataSync over the internet
- B. Snowball Edge
- C. Site-to-Site VPN
- D. S3 Transfer Acceleration

> [!success]- Answer
> **B.** 200 TB at 100 Mbps takes about 185 days. Physical transfer is the practical choice. A new customer would be directed to Data Transfer Terminal.

**5.** A company wants to archive 80 TB straight into S3 Glacier Deep Archive, using Snowball. How must this work?

- A. Set Glacier as the target on the device
- B. Import to S3, then use a lifecycle rule to move the objects
- C. Use Tape Gateway
- D. Use a Glacier vault on the device

> [!success]- Answer
> **B.** Snowball imports into S3 only. A lifecycle rule moves the objects afterwards.

**6.** An Oracle database must move to Aurora PostgreSQL, with minimal downtime. What is the correct approach? (Choose two.)

- A. Convert the schema with AWS SCT or DMS Schema Conversion
- B. Migrate the data with DMS, using full load plus CDC
- C. Use Storage Gateway
- D. Use S3 Replication
- E. Use AWS Snow Family only

> [!success]- Answer
> **A and B.** Different engines need schema conversion, and CDC keeps the source and target in step until cutover.

**7.** A company wants to move 300 on-premises Linux and Windows servers to AWS as they are, with minimal downtime. What should it use?

- A. AWS DMS
- B. AWS Application Migration Service
- C. AWS DataSync
- D. AWS Transfer Family

> [!success]- Answer
> **B.** MGN does block-level replication of whole servers for rehosting.

**8.** Which gateway keeps the primary data in AWS, with frequently accessed data stored locally, and offers iSCSI block access?

- A. Tape Gateway
- B. Volume Gateway, cached mode
- C. Volume Gateway, stored mode
- D. S3 File Gateway

> [!success]- Answer
> **B.** In cached mode, the primary copy is in AWS. In stored mode, it is local.

---
**Previous:** [[26 Infrastructure as Code and Operations]] · **Next:** [[28 High Availability and Disaster Recovery]] · **Plan:** [[Study Guide]]
