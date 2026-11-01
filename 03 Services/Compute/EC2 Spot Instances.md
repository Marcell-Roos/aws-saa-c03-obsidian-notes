---
tags: [service, cat/compute, scope/in]
aliases: ["Spot Instances", "Spot Instance", "Spot instances"]
---

# EC2 Spot Instances

- **Spot Instances**: short workloads, for cheap, can lose instances.
- Can get a discount up to 90% compared to On-demand. These are instances that you can lose at any point of time if your max price is less than the current spot price. They are not suitable for critical jobs or databases.

    Useful for workloads that are resilient to failure such as: batch jobs, data analysis, image processing, any distributed workloads …

AWS gives a **two-minute interruption notice** before reclaiming an instance. Combine Spot with On-Demand in a mixed-instances [[Amazon EC2 Auto Scaling|ASG]], and use several [[EC2 Instance Types|instance types]] to reduce interruptions.

## Exam tasks
- [[Task 4.2 Design cost-optimized compute solutions]]

---
**Up:** [[EC2 Purchasing Options]] · **Map:** [[Compute Map]]
