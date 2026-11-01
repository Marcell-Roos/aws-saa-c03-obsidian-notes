---
tags: [service, cat/containers, scope/in]
aliases: ["Karpenter"]
---

# EKS Auto Scaling

**[[Amazon EKS|EKS]] Metrics Server** - lightweight, scalable aggregator of resource usage data in our Kubernetes cluster. The primary use of the Metrics Server is to enable Horizontal Pod Autoscaling (HPA). HPA automatically adjusts the number of pod replicas in a deployment, replication controller, or [[Stateless and Stateful Workloads|stateful]] set based on observed CPU utilization.

**Kubernetes Cluster Autoscaler** automatically adjusts the size of the Kubernetes cluster (e.g. the number of nodes) based on the resource requirements of the workloads running on the cluster.

**Karpenter** - flexible, high-performance Kubernetes cluster autoscaler that launches appropriately sized compute resources, like [[Amazon EC2]] instances, in response to changing application load. It integrates with AWS to provision compute resources that precisely match workload requirements.

---
**Up:** [[Amazon EKS]] · **Map:** [[Containers Map]]
