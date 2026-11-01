---
tags: [service, cat/compute, scope/in]
aliases: ["Reserved Instances", "Reserved Instance", "Convertible Reserved Instances"]
---

# EC2 Reserved Instances

- **Reserved**: (1 & 3 years)
    - **Reserved Instances**: long workloads.

        Up to 72% discount compared to On-demand. We reserve a specific instance attributes (Instance Type, Region, Tenancy, OS). We can buy and sell in the Reserved Instance Marketplace.

        Reservation Period:

        - 1 year (Discount +)
        - 3 years (Discount +++)

        Payment Options:

        - No Upfront (Discount +)
        - Partial Upfront (Discount ++)
        - All Upfront (Discount +++)

        Reserved Instance’s scope can be regional or zonal.

    - **Convertible Reserved Instances**: long workloads with flexible instances.

        Can change the [[Amazon EC2|EC2 instance]] type, [[EC2 Instance Types|instance family]], OS, scope and tenancy. Up to 66% discount.

**Standard** RIs give the largest discount. **Convertible** RIs can change family, OS, or tenancy.

## Exam tasks
- [[Task 4.2 Design cost-optimized compute solutions]]

---
**Up:** [[EC2 Purchasing Options]] · **Map:** [[Compute Map]]
