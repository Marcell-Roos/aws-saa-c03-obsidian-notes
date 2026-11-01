---
tags: [drill, scope/in]
---

# Drill ECS EKS Fargate

Adapted from [RonitSachdev/aws-saa-c03-guides](https://github.com/RonitSachdev/aws-saa-c03-guides) (CC BY 4.0), with outdated facts changed.

## Question patterns

- *"Run containers without managing any servers or clusters of instances"* → **[[AWS Fargate|Fargate]]** (the phrase "no server management" is the trigger)
- *"Company runs Kubernetes on-premises and wants to migrate to AWS with minimal changes"* → **[[Amazon EKS|EKS]]** ("already Kubernetes" is one of only two EKS signals)
- *"[[Amazon ECS|ECS]] task fails to start; error pulling image from [[Amazon ECR|ECR]]"* → **Task Execution Role** (launch plumbing = execution role)
- *"Application inside the container gets AccessDenied calling [[Amazon DynamoDB|DynamoDB]]"* → **Task Role** (app-level permissions once running)
- *"Containerized GPU-based ML inference, minimize management"* → **ECS on [[Amazon EC2|EC2]] launch type** (Fargate has NO GPUs)
- *"Automatically scan container images for vulnerabilities"* → **ECR image scanning** (built into the registry)
- *"Assign a dedicated [[Security Groups|security group]] to each container/task"* → **awsvpc network mode** (per-task [[Elastic Network Interface|ENI]] = per-task SG)
- *"Avoid vendor lock-in / portable across clouds"* → **EKS** (Kubernetes is the portability play)
- *"Cost-optimize fault-tolerant containerized batch jobs on Fargate"* → **Fargate Spot** (interruptible = Spot)
- *"Scale container count based on messages waiting in a queue"* → **ECS Service Auto Scaling on [[Amazon SQS|SQS]] queue depth**

## Pocket card

| Keyword | Answer |
|---|---|
| "No server management" + containers | Fargate |
| "Already using Kubernetes" / "multi-cloud" | EKS |
| GPUs for containers | EC2 launch type (never Fargate) |
| Can't pull image / can't write logs | Task Execution Role |
| App AccessDenied to AWS service | Task Role |
| Recipe / blueprint | Task Definition |
| Keeps N copies running + [[Application Load Balancer\|ALB]] | Service |
| Image storage + CVE scanning | ECR |
| Per-task ENI + security group | awsvpc mode |
| Cheap interruptible Fargate | Fargate Spot |
| Multiple same-service tasks, one instance | ALB dynamic port mapping |

---
**Up:** [[Drills Map]]
