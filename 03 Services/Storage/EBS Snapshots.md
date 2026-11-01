---
tags: [service, cat/storage, scope/in]
aliases: ["EBS snapshot", "EBS Snapshot"]
---

# EBS Snapshots

It allows us to make a backup of [[Amazon EBS|EBS volume]] at a point in time. We can copy snapshots across AZ or Region. The EBS volume can be used while the snapshot is in progress.

EBS Snapshot Features:

- **EBS Snapshot Archive**

    We can move a snapshot to an “archive tier” that is 75% cheaper. It takes within 24 to 72 hours for restoring the archive.

- **Recycle Bin for EBS Snapshots**

    Setup rules to retain deleted snapshots so we can recover them after an accidental deletion.

**Fast Snapshot Restore** removes the first-read latency on restored volumes. Snapshots are incremental and stored in [[Amazon S3|S3]] behind the scenes.

---
**Up:** [[Amazon EBS]] · **Map:** [[Storage Map]]
