---
tags: [service, cat/containers, scope/in]
aliases: ["ECS", "ECS tasks", "ECS Tasks"]
---

# Amazon ECS

**ECS** [**[[Amazon EC2|EC2]] Launch Type]** - we must provision & maintain the infrastructure (EC2 instances). Each EC2 Instance must run the ECS Agent to register in the ECS Cluster. AWS takes care of starting/stopping containers.

**ECS [Fargate Launch Type]** - we do not provision the infrastructure, it’s all serverless. We just create task definitions. AWS just runs ECS Tasks for us based on the CPU/RAM we need. To scale, we just need to increase the number of tasks (no more EC2 instances).

**[[IAM Users Groups and Roles|IAM Roles]] for ECS**

- **EC2 Instance Profile** (EC2 Launch Type only) - used by ECS agent to make API calls to ECS service. We can send container logs to [[CloudWatch Logs]], pull Docker image from [[Amazon ECR|ECR]], reference sensitive data in [[AWS Secrets Manager|Secrets Manager]] or [[SSM Parameter Store]].
- **ECS Task Role** - allows each task to have a specific role. Each role can access different AWS services.

**ECS - [[Elastic Load Balancing|ELB]] Integrations**

**[[Application Load Balancer|ALB]]** - supported and works for most use cases.

**[[Network Load Balancer|NLB]]** - recommended only for high throughput/high performance use cases or to pair it with AWS Private Link.

**ECS Data Volumes ([[Amazon EFS|EFS]])**

We can mount EFS file systems onto ECS tasks. It works for both EC2 and [[AWS Fargate|Fargate]] launch types.

Tasks running in any AZ will share the same data in the EFS file system. If we use Fargate + EFS it’s totally serverless.

**Execution role versus task role:** the task execution role lets ECS pull images and write logs. The task role is what your application code uses. **ECS Express Mode** deploys containerised apps with sensible defaults. **Capacity providers** manage the EC2 or Fargate capacity behind a cluster.

## In this topic
- [[AWS App Runner]]
- [[Amazon ECR]]
- [[Amazon ECS Anywhere]]
- [[ECS Auto Scaling]]
- [[ECS Event-Driven Patterns]]

## Exam tasks
- [[Task 2.1 Design scalable and loosely coupled architectures]]
- [[Task 3.2 Design high-performing and elastic compute solutions]]

---
**Map:** [[Containers Map]]
