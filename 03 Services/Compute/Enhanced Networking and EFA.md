---
tags: [service, cat/compute, scope/in]
aliases: ["ENA", "EFA", "Elastic Fabric Adapter", "Enhanced Networking"]
---

# Enhanced Networking and EFA

**Enhanced Networking via SR-IOV (Single Root I/O Virtualization) -** a technology that allows network traffic to bypass the hypervisor and directly access the network interface card (NIC).

It’s typically used in instances that need high throughput and low latency but do not require the advanced features of ENA or EFA.

**Elastic Network Adapter (ENA)** - a custom network interface designed by AWS that supports high-performance networking. It offers better flexibility and advanced features compared to SR-IOV. ENA is suited for workloads that need higher network bandwidth (**up to 100 Gbps**).

**Elastic Fabric Adapter (EFA)** - a network interface designed for tightly coupled HPC and ML workloads that require inter-instance communication with low latency and high throughput. **EFA builds on ENA**, offering additional features like hardware-based message passing.

The OS-bypass capabilities of EFAs are not supported on Windows instances. If we attach an EFA to a Windows instance, the instance functions as an ENA without the added EFA capabilities.

**AWS ParallelCluster** is an open-source cluster management tool that simplifies the deployment and management of HPC clusters in the AWS Cloud. It allows us to easily set up a multi-node cluster for our HPC workloads. There is an ability to enable EFA on the cluster and improve network performance.

## Exam tasks
- [[Task 3.2 Design high-performing and elastic compute solutions]]

---
**Up:** [[Amazon EC2]] · **Map:** [[Compute Map]]
