---
tags: [service, cat/compute, scope/in]
aliases: ["Spot Fleet"]
---

# EC2 Spot Fleet

A set of [[EC2 Spot Instances|Spot Instances]], and optionally [[EC2 On-Demand Instances|On-Demand Instances]], launched to meet a target capacity across several instance pools. Allocation strategies:

- **capacityOptimized:** pools least likely to be interrupted
- **lowestPrice:** cheapest pools, with more interruption risk
- **diversified:** spread across pools

In practice, an [[Amazon EC2 Auto Scaling]] group with a mixed instances policy gives the same benefit.

---
**Up:** [[EC2 Purchasing Options]] · **Map:** [[Compute Map]]
