---
tags: [drill, scope/in]
---

# Drill EC2

Adapted from [RonitSachdev/aws-saa-c03-guides](https://github.com/RonitSachdev/aws-saa-c03-guides) (CC BY 4.0), with outdated facts changed.

## Question patterns

- *"Nightly batch job processes images; jobs can be re-run if they fail; minimize cost"* → **[[EC2 Spot Instances|Spot instances]]** (fault-tolerant + interruptible + cheapest = Spot's home turf)
- *"Critical payment workload, cannot tolerate interruption, minimize cost"* → **NOT Spot — [[EC2 Reserved Instances|Reserved Instances]] / [[Savings Plans|Savings Plan]]** ("cannot tolerate interruption" disqualifies Spot no matter how loudly the question says "cheapest")
- *"SAP HANA in-memory database on [[Amazon EC2|EC2]]"* → **X family** (eXtreme RAM; plain "in-memory cache/analytics" → R family)
- *"Train a deep learning model" vs "serve ML predictions cheaply"* → **P family for training, G or Inf for inference** (P = Power training, G/Inf = inference/graphics)
- *"Company has per-socket Windows Server licenses to bring to AWS"* → **[[EC2 Dedicated Hosts and Instances|Dedicated Host]]** (sockets/cores/BYOL = Host; mere hardware isolation = Dedicated Instance)
- *"Must guarantee EC2 capacity is available in a specific AZ for month-end processing"* → **Zonal Reserved Instance or On-Demand [[EC2 Capacity Reservations|Capacity Reservation]]** (Savings Plans and regional RIs are billing-only — they hold no seats)
- *"t3 instance performs well, then slows dramatically after hours of sustained load"* → **CPU credits exhausted, throttled to baseline — move to M/C family or enable Unlimited mode** (and "bill spiked after enabling a setting" = Unlimited overage)
- *"After stopping and starting the instance, users can't reach it at the old address"* → **Public IP changed on stop/start — assign an Elastic IP** (default public IPs are not sticky)
- *"On primary failure, standby must take over with the same private IP, no client changes"* → **Move the [[Elastic Network Interface|ENI]] to the standby** (works only within the **same AZ**)
- *"Tightly-coupled HPC workload needs the lowest inter-node latency"* → **Cluster [[EC2 Placement Groups|placement group]]** (Close = same rack; Kafka/Cassandra/Hadoop at scale = Partition; 7 critical solo instances = Spread)
- *"Steady $ commitment but wants freedom to switch families, regions, and even [[AWS Fargate|Fargate]]/Lambda"* → **Compute Savings Plan** (one family, one region, max discount = EC2 Instance Savings Plan)
- *"Predictable baseline + unpredictable spikes, optimize cost"* → **RI/Savings Plan for baseline + Spot for the spikes** (the classic combo)

## Pocket card

| Keyword | Answer |
|---|---|
| general purpose / balanced | M family |
| spiky, mostly idle / CPU credits | T family (burstable) |
| t3 slow after sustained load | credits exhausted → M/C family or Unlimited mode |
| bill increased during spike | T Unlimited mode overage |
| batch / encoding / HPC compute | C family |
| in-memory analytics / cache | R family |
| SAP HANA | X family |
| high local NVMe IOPS | I family |
| dense local HDD storage | D family |
| ML training | P family (GPU) |
| graphics / ML inference | G family / Inf |
| price-performance / cost / sustainability + ARM-friendly | Graviton (g suffix, e.g. m7g) |
| short-term, unpredictable, < 1 year | On-Demand |
| steady 24/7 for 1–3 years | Reserved Instance (up to 72%) |
| RI but family may change | Convertible RI (66%) |
| guarantee capacity in an AZ | Zonal RI / Capacity Reservation |
| commit $/hr, any family/region + Fargate/Lambda | Compute Savings Plan |
| commit $/hr, one family one region, max discount | EC2 Instance Savings Plan |
| interruptible / fault-tolerant / cheapest (up to 90%) | Spot (2-min warning) |
| database / cannot tolerate interruption | never Spot |
| baseline + surge, optimize cost | RI/SP baseline + Spot surge |
| BYOL / per-socket / per-core licenses | Dedicated Host |
| hardware isolation only, cheaper | Dedicated Instance |
| lowest latency / HPC / same rack | Cluster placement group |
| few critical instances, isolate failures (max 7/AZ) | Spread placement group |
| Hadoop / Cassandra / Kafka at scale | Partition placement group |
| failover keeping same private IP (same AZ) | move the ENI |
| separate management network / dual-homed | multiple ENIs |
| public IP changed after stop/start | Elastic IP |
| avoid EIPs / static entry point best practice | [[Elastic Load Balancing\|ELB]] + [[DNS Fundamentals\|DNS]] or [[AWS Global Accelerator\|Global Accelerator]] |
| run script once at launch | user data (runs as root) |
| instance info from inside / SSRF protection | metadata at 169.254.169.254 / enforce IMDSv2 |
| preserve RAM state across stop | [[EC2 Hibernate\|Hibernate]] (RAM → encrypted [[Amazon EBS\|EBS]] root) |

---
**Up:** [[Drills Map]]
