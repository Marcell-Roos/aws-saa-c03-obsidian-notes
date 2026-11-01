---
tags: [service, cat/containers, scope/in]
aliases: ["EKS"]
---

# Amazon EKS

**EKS** is a managed service that simplifies the process of running Kubernetes on AWS. It is an alternative to [[Amazon ECS|ECS]], similar goal but different API. Kubernetes is cloud-agnostic (can be used in any cloud).

EKS supports [[Amazon EC2|EC2]] if we want to deploy worker nodes or [[AWS Fargate|Fargate]] to deploy serverless containers.

We can attach data volumes to our EKS cluster. We need to specify StorageClass manifest on our EKS cluster. It leverages a **Container Storage Interface (CSI)** compliant driver.

We have support for [[Amazon EBS|EBS]], [[Amazon EFS|EFS]] (works with Fargate), [[FSx for Lustre]], [[FSx for NetApp ONTAP]].

**Amazon EKS Connector** is a feature that allows us to connect and manage Kubernetes clusters running outside of AWS (whether on-premises or in other cloud environments) within the Amazon EKS console.

**[[Amazon EKS Anywhere]]** is a deployment option for Amazon EKS that enables us to create and operate Kubernetes clusters on our own infrastructure, such as on-premises data centers or other cloud environments.

**EKS Node Types**

- **Managed Node Groups** - creates and manages Nodes (EC2 instances) for us. Nodes are part of an [[Amazon EC2 Auto Scaling|ASG]] managed by EKS. It supports on-demand or spot instances.
- **Self-Managed Nodes** - nodes created by us and registered to the EKS cluster and managed by an ASG. We can use prebuilt [[Amazon Machine Image|AMI]] (EKS Optimized AMI). It supports on-demand or spot instances.
- **AWS Fargate** - no maintenance required, no nodes managed.

**EKS Auto Mode** extends AWS management to compute, storage and networking in the cluster. **EKS Connector** registers outside clusters for viewing in the console.

## In this topic
- [[Amazon EKS Anywhere]]
- [[Amazon EKS Distro]]
- [[EKS Auto Scaling]]
- [[EKS Security]]

## Exam tasks
- [[Task 2.1 Design scalable and loosely coupled architectures]]
- [[Task 3.2 Design high-performing and elastic compute solutions]]

---
**Map:** [[Containers Map]]
