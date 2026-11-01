---
tags: [drill, scope/in]
---

# Drill Snow Family

Adapted from [RonitSachdev/aws-saa-c03-guides](https://github.com/RonitSachdev/aws-saa-c03-guides) (CC BY 4.0), with outdated facts changed.

## Question patterns

- *"Research ship must run analysis on collected data with no internet connectivity"* → **[[AWS Snow Family|Snowball Edge]] Compute Optimized** (compute at the disconnected edge; GPU if ML is mentioned)
- *"Company wants to archive 80 TB directly into [[Amazon S3 Glacier|S3 Glacier]] using Snowball"* → **Import to [[Amazon S3|S3]], then [[S3 Lifecycle Rules|lifecycle rule]] to Glacier** (Snowball can't write to Glacier directly — THE trap)
- *"Transfer 40 TB once; would take 6 weeks over the existing connection"* → **Snowball Edge** (>1 week over the wire → Snow family)
- *"Manage Snow devices with a graphical interface"* → **AWS OpsHub** (the Snow GUI)

## Pocket card

| Keyword | Answer |
|---|---|
| Transfer would take > 1 week | Snow family |
| 50–500 TB migration | Snowball Edge Storage Optimized |
| Process data offline / GPU at edge | Snowball Edge Compute Optimized |
| Straight to Glacier? | No — S3 first + lifecycle rule |
| Encryption on device | [[AWS KMS\|KMS]], automatic |
| GUI for Snow devices | OpsHub |

---
**Up:** [[Drills Map]]
