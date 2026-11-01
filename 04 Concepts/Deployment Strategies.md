---
tags: [concept, scope/in]
aliases: ["Blue-Green", "Canary Deployment", "Rolling Deployment", "blue/green"]
---

# Deployment Strategies

**All-at-Once (Big Bang)** - deploys the new version of the application to all instances at once. It is simple and fast, with no need for complex infrastructure setups. It has high risk of downtime if the new version has issues, no easy rollback. If something goes wrong, the entire system can be affected.

Use Cases: **Non-critical applications where downtime is acceptable** **or where rollback procedures are straightforward**.

**Rolling Deployment** - gradually replaces instances of the old version with instances of the new version. Reduces the risk of full-scale failure and can be quickly fixed or rolled back.

Use Cases: **Applications that need to minimize downtime but can tolerate temporary inconsistencies**.

**Blue-Green Deployment** - two identical environments are maintained: one (blue) running the current version and another (green) running the new version. Traffic is switched from the blue environment to the green one once the new version is ready.

It is zero-downtime deployment, easy rollback by switching traffic back to the blue environment. Testing and validation can be done on the green environment.

Use Cases: **Applications requiring zero downtime and where rollback needs to be swift and reliable**.

**Canary Deployment** - small portion of the traffic is directed to the new version while the rest remains on the old version. Gradually, more traffic is shifted to the new version as confidence in its stability grows. It allows for real-world testing with minimal risk.

Use Cases: Applications with a **large user base or critical services where early feedback and incremental rollout are important**.

**A/B Testing Deployment** - similar to Canary deployment, but with a focus on running two or more versions simultaneously to compare performance or user experience. Different users are directed to different versions.

Use Cases: **Testing new features, UI/UX changes, or optimizations**.

**Shadow Deployment** - new version is deployed alongside the old version, but the new version does not serve production traffic. Instead, it processes a copy of the production traffic to see how it behaves.

Use Cases: Validating major updates or entirely new services without risking production stability.

---
**Up:** [[Home]]
