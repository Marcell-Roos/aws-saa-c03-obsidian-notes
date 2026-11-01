---
tags: [service, cat/compute, scope/in]
aliases: ["instance types", "instance family"]
---

# EC2 Instance Types

The source had this only as an image.

| Family | Letter examples | Optimised for | Use |
| --- | --- | --- | --- |
| General purpose | M, T | Balance | Web servers, small databases. T is burstable |
| Compute optimized | C | CPU | Batch, HPC, gaming, encoding |
| Memory optimized | R, X | RAM | In-memory databases, caches |
| Storage optimized | I, D | Local disk IOPS | NoSQL, data warehousing |
| Accelerated computing | P, G, Inf, Trn | GPUs or ML chips | ML, graphics |
| HPC optimized | Hpc | Tightly coupled compute | Simulations |

Name format: in `m7g.large`, `m` is the family, `7` the generation, `g` the attribute (Graviton) and `large` the size. Graviton usually gives the best price performance.

## Exam tasks
- [[Task 3.2 Design high-performing and elastic compute solutions]]
- [[Task 4.2 Design cost-optimized compute solutions]]

---
**Up:** [[Amazon EC2]] · **Map:** [[Compute Map]]
