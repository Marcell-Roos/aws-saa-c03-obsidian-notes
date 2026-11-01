---
tags: [service, cat/storage, scope/in]
aliases: ["gp3", "gp2", "io2 Block Express", "st1", "sc1"]
---

# EBS Volume Types

[[Amazon EBS|EBS]] Volumes are characterized in size, throughput and IOPS. Only SSD volumes (gp2, gp3, io1, io2 Block Express) can be boot volumes. st1 and sc1 can't.

- **gp2 / gp3 (SSD)** - general purpose SSD volume that balances price and performance for a wide variety of workloads. Small gp2 volume can burst IOPS to 3000. Gp3 is cheaper.
- **io1 / io2 Block Express (SSD)** - highest performance SSD volume for mission-critical low-latency or high-throughput workloads. Supports multi-attach. It’s great for database workloads.

- **st1 (HDD)** - low cost HDD volume designed for frequently accessed, throughput-intensive workloads.
- **sc1 (HDD)** - lowest cost HDD volume designed for less frequently accessed workloads.

| Type | Size | Max IOPS | Max throughput | Use |
| --- | --- | --- | --- | --- |
| gp3 | 1 GiB to 64 TiB | 80,000 | 2,000 MiB/s | Default choice. Baseline 3,000 IOPS and 125 MiB/s |
| io2 Block Express | Up to 64 TiB | 256,000 | See docs | Critical databases, 99.999% durability |
| st1 | 0.125 to 16 TiB | N/A | 500 MiB/s | Big data, logs |
| sc1 | HDD | N/A | Lower | Cold data, lowest cost |

gp3 sets IOPS and throughput separately from size, and it doesn't burst. Older guides quote 16,000 IOPS for gp3, which is out of date.

## Exam tasks
- [[Task 3.1 Determine high-performing and or or scalable storage solutions]]
- [[Task 4.1 Design cost-optimized storage solutions]]

---
**Up:** [[Amazon EBS]] · **Map:** [[Storage Map]]
