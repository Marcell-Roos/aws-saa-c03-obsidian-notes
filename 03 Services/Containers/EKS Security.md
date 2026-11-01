---
tags: [service, cat/containers, scope/in]
---

# EKS Security

[[Amazon EKS|EKS]] uses [[AWS IAM|IAM]] to provide authentication to our Kubernetes cluster, but it still relies on native Kubernetes Role-Based Access Control (RBAC) for authorization. This means that IAM is only used for the authentication of valid IAM entities. All permissions for interacting with our Amazon EKS cluster’s Kubernetes API are managed through the native Kubernetes RBAC system.

**Access entries** are now the recommended way to map IAM principals to Kubernetes permissions. The older `aws-auth` ConfigMap is legacy, so the source's detail on it was removed.

**IRSA** and **EKS Pod Identity** give pods their own IAM permissions.

---
**Up:** [[Amazon EKS]] · **Map:** [[Containers Map]]
