---
tags: [service, cat/compute, scope/in]
aliases: ["EC2", "EC2 instance", "EC2 instances", "EC2 Instances"]
---

# Amazon EC2

EC2 is an IaaS that offer:

- Renting virtual machines (EC2 Instances)
- Storing data on virtual drives ([[Amazon EBS|EBS]])
- Distribute load across machines ([[Elastic Load Balancing|ELB]])
- Scale the services using an auto-scaling group ([[Amazon EC2 Auto Scaling|ASG]])

When we create EC2 we can configure OS, CPU, RAM, storage, network card, security and bootstrap script.

**Bootstrap script** is a configuration script that runs at first launch. Bootstrapping instances is done by using **EC2 User Data** script (**runs with root user privileges**).

**Instance metadata** is data about our EC2 instance that we can use to configure or manage the running instance. Because our instance metadata is available from our running instance, we do not need to use the EC2 console or the [[AWS CLI]]. This can be helpful when we're writing scripts to run from your instance.

**Instance metadata:** IMDSv2 is the session-oriented, safer version. Require it where possible. Instance roles are delivered through metadata, so never store [[AWS Access Methods|access keys]] on an instance.

**Pricing and sizes:** see [[EC2 Instance Types]] and [[EC2 Purchasing Options]].

## In this topic
- [[Amazon Machine Image]]
- [[EC2 Hibernate]]
- [[EC2 Image Builder]]
- [[EC2 Instance Connect]]
- [[EC2 Placement Groups]]
- [[Elastic Network Interface]]
- [[Enhanced Networking and EFA]]
- [[Instantiating Applications Quickly]]

## Exam tasks
- [[Task 3.2 Design high-performing and elastic compute solutions]]

---
**Map:** [[Compute Map]]
