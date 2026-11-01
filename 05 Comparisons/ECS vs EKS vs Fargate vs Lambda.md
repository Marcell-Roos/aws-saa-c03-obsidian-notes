---
tags: [comparison, scope/in]
---

# ECS vs EKS vs Fargate vs Lambda

| | [[Amazon ECS]] | [[Amazon EKS]] | [[AWS Fargate]] | [[AWS Lambda]] |
| --- | --- | --- | --- | --- |
| What | AWS container orchestrator | Managed Kubernetes | Serverless hosts for [[Amazon ECS\|ECS]] or [[Amazon EKS\|EKS]] | Functions |
| Portability | AWS | Any Kubernetes | Depends | AWS |
| Max runtime | None | None | None | 15 minutes |
| Choose when | Simple AWS-native containers | Existing Kubernetes skills | No hosts to manage | Short [[Event-Driven Architecture\|event-driven]] code |

## Exam tasks
- [[Task 4.2 Design cost-optimized compute solutions]]

---
**Up:** [[Comparisons Map]]
