---
tags: [drill, scope/in]
---

# Drill StorageGateway DataSync TransferFamily

Adapted from [RonitSachdev/aws-saa-c03-guides](https://github.com/RonitSachdev/aws-saa-c03-guides) (CC BY 4.0), with outdated facts changed.

## Question patterns

- *"Company wants to eliminate its physical tape backup infrastructure but keep existing backup software"* → **[[AWS Storage Gateway|Tape Gateway]]** (virtual tape library → [[Amazon S3|S3]]/Glacier; software sees tapes).
- *"Replace an aging NAS; store files in S3 but keep low-latency local access over SMB/NFS"* → **S3 File Gateway** (cloud-backed share with local cache).
- *"Migrate 50 TB from an on-prem NAS to S3, preserving file permissions and metadata, minimal effort"* → **[[AWS DataSync|DataSync]]** (migration engine; preserves metadata; gateway is for ongoing access, not moves).
- *"Business partners upload files via SFTP and cannot change their workflow; files must land in S3"* → **[[AWS Transfer Family|Transfer Family]]** (managed SFTP endpoint — never build SFTP on [[Amazon EC2|EC2]]).
- *"On-prem app needs low-latency access to the ENTIRE dataset, with backups to AWS for DR"* → **Volume Gateway — Stored** (full data local, async snapshots to S3).
- *"On-prem storage is running out of space; extend capacity while keeping frequently used data fast"* → **Volume Gateway — Cached** (primary in S3, hot cache local).
- *"Copy files nightly from on-prem SMB shares to [[Amazon EFS|EFS]], with bandwidth [[Service Quotas and Throttling|throttling]]"* → **DataSync** (scheduled transfers + throttling are its signature features).
- *"Transfer data between S3 and EFS within AWS"* → **DataSync** (works AWS-to-AWS too, agentless).

## Pocket card

| Keyword | Answer |
|---|---|
| Replace tape backups | Tape Gateway (VTL → S3/Glacier) |
| NAS replacement, files in S3, local access | S3 File Gateway |
| Extend on-prem capacity, primary in cloud | Volume Gateway — Cached |
| Full dataset local + snapshots to cloud | Volume Gateway — Stored |
| Migrate / scheduled sync, preserve permissions | DataSync |
| Bandwidth throttling, on-prem agent | DataSync |
| S3 ↔ EFS ↔ [[Amazon FSx\|FSx]] transfers | DataSync |
| Partners upload via SFTP/FTPS/FTP | Transfer Family (never SFTP-on-EC2) |
| Ongoing hybrid access vs. one-time move | Storage Gateway vs. DataSync |
| Offline / massive data, no bandwidth | [[AWS Snow Family\|Snow Family]] (Section 27) |

---
**Up:** [[Drills Map]]
