---
tags: [service, cat/storage, scope/in]
aliases: ["EBS", "EBS volume", "EBS volumes", "EBS Volume"]
---

# Amazon EBS

**EBS Volume** (think of them as a “network USB stick”) is a network drive we can attach to our instances (cloud only) while they run. It allows our instances to persist data even after their termination. EBS volumes support live configuration changes while in production which means that we can modify the volume type, volume size, and IOPS capacity without service interruptions.

EBS can only be mounted to one instance at a time. They are bound to a specific AZ.

**Data Lifecycle Manager (DLM)** - automate the creation, retention, and deletion of snapshots taken to back up our EBS volumes.

**Delete on Termination**

- Controls the EBS behaviour when an [[Amazon EC2|EC2 instance]] terminates.
    - By default, the root EBS volume is deleted (attribute enabled).
    - By default, any other attached EBS volume is not deleted (attribute disabled).
- This can be controlled by the AWS console / [[AWS CLI]].
- Use case: preserve root volume when instance is terminated.

## In this topic
- [[EBS Encryption]]
- [[EBS Multi-Attach]]
- [[EBS Snapshots]]
- [[EBS Volume Types]]
- [[EC2 Instance Store]]
- [[RAID Configurations]]

## Exam tasks
- [[Task 3.1 Determine high-performing and or or scalable storage solutions]]

---
**Map:** [[Storage Map]]
