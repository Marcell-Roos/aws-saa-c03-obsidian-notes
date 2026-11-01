---
tags: [service, cat/compute, scope/in]
aliases: ["hibernation", "Hibernate"]
---

# EC2 Hibernate

**Hibernate** is a feature designed to help us manage our [[Amazon EC2|EC2 instances]] more efficiently by allowing us to pause and resume them. When we hibernate an instance, the contents of its memory (RAM) are saved to an [[Amazon EBS|EBS volume]], and the instance is stopped rather than terminated. We can later resume the instance from this saved state. The root EBS volume must be encrypted.

Hibernation is useful for workloads that don’t require continuous operation but need to be quickly resumed.

Limits: Linux instances need under 150 GiB of RAM, and Windows instances 16 GiB or less. The root volume must be EBS, encrypted, and large enough to hold the RAM contents.

## Exam tasks
- [[Task 4.2 Design cost-optimized compute solutions]]

---
**Up:** [[Amazon EC2]] · **Map:** [[Compute Map]]
