---
tags: [concept, scope/in]
aliases: ["immutable infrastructure"]
---

# Immutable Infrastructure

Replace servers instead of changing them. Bake a new [[Amazon Machine Image]], roll it out with [[Amazon EC2 Auto Scaling]], and roll back by pointing at the old version. This prevents configuration drift and makes deployments repeatable. [[AWS CloudFormation]] and [[EC2 Image Builder]] support the approach. See [[Deployment Strategies]].

## Exam tasks
- [[Task 2.2 Design highly available and or or fault-tolerant architectures]]

---
**Up:** [[Concepts Map]]
