---
tags: [service, cat/migration, scope/in]
---

# On-Premises Strategies

- **Amazon Linux VM images** - run Amazon Linux on-premises. AL2023 ships KVM (qcow2), VMware (OVA) and Hyper-V (vhdx) images.
- **VM Import/Export** - migrate existing applications into [[Amazon EC2|EC2]], create a DR repository strategy for our on-premise VMs. Can export back the VMs from EC2 to on-premise.
- **[[AWS Application Discovery Service]]** - gather information about our on-premise servers to plan a migration.
- **[[AWS DMS|AWS Database Migration Service]]** - replicate on-premise ⇒ AWS, AWS ⇒ AWS, AWS ⇒ on-premise.
- **[[AWS Application Migration Service]] (MGN)** - replicates live servers to AWS. It replaced the Server Migration Service, which shut down on 1 April 2023.

---
**Map:** [[Migration and Transfer Map]]
