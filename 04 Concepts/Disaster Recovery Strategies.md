---
tags: [concept, scope/in]
aliases: ["disaster recovery", "Disaster Recovery", "Pilot Light", "Warm Standby", "Backup and Restore"]
---

# Disaster Recovery Strategies

**Disaster Recovery Strategies**

- **Backup & Restore** - most basic DR strategy where data is backed up to AWS storage services and restored in the event of a disaster. Suitable for non-critical applications where downtime can be tolerated.

    [[RPO and RTO|RTO]] and RPO are typically longer because the restoration process involves re-provisioning infrastructure and retrieving data.

- **Pilot Light** - a minimal version of an environment is always running in AWS, which can be scaled up to a full-scale production environment when needed. Suitable for critical applications where a minimal version can handle some traffic until full scaling occurs.

    Faster than the backup and restore strategy but still involves some time for scaling up and provisioning additional resources. The RPO can be near real-time since core components are active.

- **Warm Standby** - a scaled-down version of a fully functional environment is running in AWS, which can be quickly scaled up to handle production load. Suitable for critical applications requiring reduced RTO and RPO.

- **Multi-Site (Hot-Site)** - the most robust DR strategy where multiple active sites run simultaneously, providing full redundancy and load balancing. Suitable for mission-critical applications requiring near-zero downtime and [[Scalability and High Availability|high availability]].

    This approach offers the lowest RTO and RPO, potentially near zero, as both sites are live and in sync.

**Disaster Recovery Strategies Comparison**

See [[DR Strategies Compared]] and [[Pattern Multi-Region Active-Passive]].

## In this topic
- [[AWS Elastic Disaster Recovery]]
- [[RPO and RTO]]

## Exam tasks
- [[Task 2.2 Design highly available and or or fault-tolerant architectures]]

---
**Up:** [[Home]]
