---
tags: [drill, scope/in]
---

# Drill EBS EFS InstanceStore

Adapted from [RonitSachdev/aws-saa-c03-guides](https://github.com/RonitSachdev/aws-saa-c03-guides) (CC BY 4.0), with outdated facts changed.

## Question patterns

- *"Database needs 12,000 IOPS, cost-effective"* → **[[EBS Volume Types|gp3]]** (gp3 now reaches 80,000 IOPS, and provisions IOPS cheaply)
- *"Critical database needs 50,000 IOPS"* → **io1/io2** (critical and sustained I/O points to io2 Block Express, up to 256,000 IOPS)
- *"Sequential processing of large log files, throughput-focused, cost-effective"* → **st1** (big + sequential = HDD; frequent access = st1, cold archive = sc1 — and neither can boot)
- *"gp2 volume needs more IOPS but not more storage"* → **migrate to gp3** (gp2 chains IOPS to size; gp3 provisions them independently and is ~20% cheaper)
- *"Fleet of Linux instances in an [[Amazon EC2 Auto Scaling|ASG]] must share uploaded files"* → **[[Amazon EFS|EFS]]** (many mounters + multi-AZ + NFS = the shared folder)
- *"Windows instances need shared storage with Active Directory integration"* → **[[FSx for Windows File Server]]** (EFS is Linux-only — THE trap)
- *"Fastest possible storage for temporary scratch/cache data"* → **[[EC2 Instance Store|Instance Store]]** ("temporary" unlocks it; millions of IOPS, ephemeral is fine here)
- *"High IOPS storage whose data must persist after the instance stops"* → **io2 [[Amazon EBS|EBS]], not instance store** ("persist" disqualifies the notepad)
- *"Data volume must survive instance termination"* → **DeleteOnTermination = false** (root defaults true, extra volumes default false — check which one the question means)
- *"Encrypt an existing unencrypted EBS volume"* → **snapshot → copy with encryption enabled → create volume from the encrypted copy** (no in-place flip exists)
- *"Back up EBS volumes to another region for DR, automatically"* → **DLM-scheduled snapshots + cross-region snapshot copy** (snapshots live in [[Amazon S3|S3]] and copy across regions)
- *"Multiple instances must attach the same block volume in one AZ (cluster software)"* → **io1/io2 [[EBS Multi-Attach|Multi-Attach]]** (up to 16 instances, same AZ — [[Storage Types|block storage]], not a file system)
- *"Reduce cost of EFS for files untouched for months"* → **[[S3 Lifecycle Rules|lifecycle policy]] to EFS IA/Archive** (same trick as S3 tiering, applied to the shared folder)

## Pocket card

| Keyword | Answer |
|---|---|
| random I/O / database / boot volume | SSD (gp3 or io1/io2) |
| large sequential / big data / throughput MB/s | HDD (st1/sc1) — never bootable |
| Up to 80,000 IOPS, general use | gp3 |
| Sub-millisecond or critical I/O | io2 Block Express |
| 256,000 IOPS / sub-millisecond | io2 Block Express |
| frequent sequential (logs, ETL) | st1 |
| coldest, cheapest EBS | sc1 |
| gp2 mentioned at all | migrate to gp3 (~20% cheaper) |
| more IOPS without more storage | gp3 (independent provisioning) |
| multiple instances, one block volume, same AZ | io1/io2 Multi-Attach (max 16) |
| root disk survives termination | DeleteOnTermination = false |
| new extra volume unusable | format + mount + fstab |
| move volume across AZ/region | snapshot → (copy) → restore |
| cheap rarely-restored snapshots | Snapshot Archive (75% off, 24–72 hr restore) |
| recover deleted snapshot | Recycle Bin |
| instant full performance from snapshot | Fast Snapshot Restore (expensive) |
| automate snapshot schedules | Data Lifecycle Manager |
| encrypt existing volume | snapshot → copy-encrypted → restore |
| shared files, many Linux instances, multi-AZ | EFS (NFS, pay per GB used) |
| shared files, Windows / SMB / Active Directory | FSx for Windows (never EFS) |
| HPC parallel file system | [[FSx for Lustre]] |
| thousands of concurrent EFS clients | Max I/O performance mode |
| EFS throughput default | Elastic mode |
| cut EFS cost on cold files | lifecycle to IA / Archive |
| fastest storage / temp / cache / scratch | Instance Store (ephemeral) |
| instance store + stop/terminate | data gone (reboot survives) |
| high IOPS + must persist | io2 EBS, not instance store |
| Cassandra/replicated data, local speed | Instance Store is OK |

---
**Up:** [[Drills Map]]
