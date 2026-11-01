---
tags: [drill, scope/in]
---

# Drill FSx

Adapted from [RonitSachdev/aws-saa-c03-guides](https://github.com/RonitSachdev/aws-saa-c03-guides) (CC BY 4.0), with outdated facts changed.

## Question patterns

- *"Windows applications need shared storage with Active Directory authentication"* → **[[FSx for Windows File Server]]** (SMB + AD = Windows [[Amazon FSx|FSx]]; [[Amazon EFS|EFS]] can't do Windows)
- *"ML training job needs high-throughput access to a dataset stored in [[Amazon S3|S3]]"* → **[[FSx for Lustre]]** (only Lustre mounts S3 as a filesystem at HPC speed)
- *"Migrate on-premises NetApp storage to AWS with minimal changes"* → **[[FSx for NetApp ONTAP]]** (the word "NetApp" is the whole answer)
- *"Short-term, cost-optimized high-performance storage for a batch processing job"* → **FSx for Lustre Scratch** (temporary + cheap + no replication = Scratch)
- *"File share accessed by both Linux (NFS) and Windows (SMB) clients"* → **FSx for NetApp ONTAP** (the only multi-protocol option)
- *".NET application storing user home directories, must survive AZ failure"* → **FSx for Windows, Multi-AZ** (Windows workload + HA = Multi-AZ Windows FSx)
- *"Replace an on-prem ZFS file server serving NFS to Linux clients"* → **[[FSx for OpenZFS]]** (ZFS named → OpenZFS)

## Pocket card

| Keyword | Answer |
|---|---|
| Windows / SMB / NTFS / AD / .NET | FSx for Windows File Server |
| HPC / ML training / rendering / GB/s | FSx for Lustre |
| Process S3 data as files | FSx for Lustre (S3 integration) |
| Temporary + cheapest Lustre | Scratch deployment |
| Long-term Lustre | Persistent deployment |
| NetApp / SnapMirror | FSx for NetApp ONTAP |
| NFS + SMB + iSCSI together | FSx for NetApp ONTAP |
| ZFS | FSx for OpenZFS |
| Plain Linux shared storage | EFS (not FSx at all) |

---
**Up:** [[Drills Map]]
