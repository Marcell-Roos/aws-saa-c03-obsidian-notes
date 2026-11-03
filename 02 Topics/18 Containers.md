---
tags: [topic, cat/compute, scope/in]
aliases: ["Amazon ECS", "ECS", "Amazon ECS Anywhere", "ECS Auto Scaling", "ECS Event-Driven Patterns", "Amazon EKS", "EKS", "Amazon EKS Anywhere", "Amazon EKS Distro", "EKS Auto Scaling", "EKS Security", "AWS Fargate", "Fargate", "Amazon ECR", "ECR", "AWS App Runner", "ECS vs EKS vs Fargate vs Lambda", "Drill ECS EKS Fargate"]
---

# Containers

> [!info] Why this matters
> [[Domain 2 Design Resilient Architectures#Task 2.1|Task 2.1]] asks when to use containers, how to migrate into them, and how they are orchestrated. Containers also appear in [[Domain 3 Design High-Performing Architectures#Task 3.2|Task 3.2]] and [[Domain 4 Design Cost-Optimized Architectures#Task 4.2|Task 4.2]]. Most questions come down to ECS or EKS, Fargate or EC2, and task role or execution role.
>
> **Study time:** about 2.5 hours.

## Containers in brief

A **container** packages an application with its dependencies, so that it runs the same everywhere. Unlike a VM, it shares the host's kernel, so it starts in seconds and uses less memory. An **image** is the template, and a **container** is a running image.

An **orchestrator** decides where containers run, restarts failed ones and scales them.

| | Amazon ECS | Amazon EKS | AWS Fargate | AWS Lambda |
| --- | --- | --- | --- | --- |
| What | AWS's own orchestrator | Managed Kubernetes | Serverless hosts for ECS or EKS | Functions |
| Portability | AWS | Any Kubernetes | Depends on the orchestrator | AWS |
| Maximum run time | None | None | None | 15 minutes |
| Choose when | Simple AWS-native containers | Existing Kubernetes skills, multi-cloud | No hosts to manage | Short event-driven code |

### Moving an application into containers

1. Package the application and its dependencies into an image, using a Dockerfile.
2. Push the image to Amazon ECR.
3. Move state out of the container: sessions to ElastiCache or DynamoDB, files to S3 or EFS, data to a managed database.
4. Run it on ECS or EKS, usually on Fargate, behind an Application Load Balancer.
5. Pass in configuration through environment variables and secrets, and not in the image.

## Amazon ECR

**Elastic Container Registry** stores container images, as a private or public registry. It is backed by S3.

- Access is controlled through IAM.
- **Image scanning** finds vulnerabilities, using basic scanning or enhanced scanning through Amazon Inspector.
- **Lifecycle policies** remove old images.
- Replication works across Regions and accounts.

## Amazon ECS

**Elastic Container Service** is AWS's own container orchestrator.

| Term | Meaning |
| --- | --- |
| **Cluster** | A logical group of capacity |
| **Task definition** | The blueprint: image, CPU, memory, roles, ports |
| **Task** | A running copy of a task definition |
| **Service** | Keeps a set number of tasks running, and connects them to a load balancer |

### Where tasks run

| Capacity | You manage | Notes |
| --- | --- | --- |
| **Fargate** | Nothing but the task | Serverless. To scale, add tasks |
| **EC2** | The instances | Each instance runs the ECS agent. Needed for GPUs and full host control |
| **ECS Managed Instances** | Little | AWS manages EC2 capacity for you |
| **ECS Anywhere** | Your own servers | AWS hosts the control plane |

**Capacity providers** manage the capacity behind a cluster, and scale the EC2 Auto Scaling group automatically. **ECS Express Mode** deploys containerised apps with sensible defaults.

### IAM roles for ECS

This is the most-tested ECS detail.

| Role | Used by | For |
| --- | --- | --- |
| **Task execution role** | ECS | Pulling images from ECR, writing logs, fetching secrets at start-up |
| **Task role** | Your application code | Calling AWS services, such as DynamoDB |
| **EC2 instance profile** | ECS agent on EC2 hosts | Talking to the ECS service |

If a task **cannot start** or pull an image, check the execution role. If the app gets **AccessDenied** calling AWS, check the task role.

### Networking and load balancing

- **awsvpc mode** gives each task its own network interface, so that each task can have its own security group. It is required for Fargate.
- An **ALB** suits most services, and dynamic port mapping lets many tasks run on one instance.
- An **NLB** suits very high throughput, or PrivateLink.
- **ECS Service Connect** lets services reach each other by short names, with service discovery and a service mesh built in. AWS points App Mesh users to it.

| Network mode | Behaviour |
| --- | --- |
| **awsvpc** | Each task gets its own interface. Required on Fargate, and recommended elsewhere |
| **bridge** | Docker's virtual network, with port mapping on EC2 |
| **host** | Tasks share the host's network directly |

### Storage

- **EFS** gives shared persistent storage across tasks in any AZ, and it works with Fargate and EC2. Fargate plus EFS is fully serverless.
- Fargate tasks get 20 GiB of ephemeral storage by default, and up to 200 GiB.
- ECS can attach one **EBS volume** to a task, including Linux tasks on Fargate, for storage-heavy work. It is not shared between tasks.

### Passing secrets to tasks

Reference a Secrets Manager secret or a Parameter Store parameter in the **task definition**. ECS fetches it at start-up, and passes it in as an environment variable. This uses the **task execution role**, so that role needs permission to read the secret. If the application fetches a secret itself while running, the **task role** needs the permission.

### Placing tasks on EC2

On the EC2 launch type you can choose how tasks are placed. Fargate handles this for you.

| Strategy | Effect | Use |
| --- | --- | --- |
| **binpack** | Fills instances on CPU or memory | Lowest cost, with fewer instances |
| **spread** | Spreads across AZs or instances | Highest availability |
| **random** | Places randomly | Simple cases |

**Constraints** add rules: `distinctInstance` puts each task on a different instance, and `memberOf` limits tasks to instances that match an expression.

### Deployments

A rolling update replaces tasks gradually, using minimum and maximum healthy percentages. The **deployment circuit breaker** stops a failing deployment and rolls it back.

### Auto scaling

**ECS Service Auto Scaling** changes the number of tasks, using target tracking, step or scheduled scaling. It works at the task level, while EC2 Auto Scaling works at the instance level. On Fargate you scale only tasks. On EC2 you also need to scale instances, ideally with a capacity provider.

To scale workers on a queue, use the SQS queue depth metric.

### Event-driven patterns

| Pattern | How |
| --- | --- |
| **Task on an event** | An EventBridge rule runs a Fargate task when an object lands in S3 |
| **Task on a schedule** | An EventBridge schedule runs a task for batch work |
| **Queue workers** | A service polls SQS, processes messages, and failed messages go to a DLQ |
| **React to stopped tasks** | EventBridge catches ECS task state changes, and alerts through SNS or Lambda |

## AWS Fargate

**Fargate** runs containers with no hosts to manage, on ECS or EKS. You set CPU and memory per task, and pay for those resources while the task runs.

- It costs more per vCPU than well-used EC2, but needs no patching and has no idle capacity.
- **Fargate Spot** is a cheaper option for interruptible tasks, with a two-minute warning. It works on ECS, not EKS.
- Compute Savings Plans cover Fargate.
- It does not support GPUs, so GPU containers need EC2.
- Each task has its own isolation boundary and does not share a kernel, CPU resources, memory or network interface with other tasks, so choose it for isolation and security as well as convenience.

## Amazon EKS

**Elastic Kubernetes Service** is managed Kubernetes. AWS runs the control plane, across multiple AZs. Kubernetes is open source and cloud-agnostic, so EKS is the answer when a company **already uses Kubernetes** or wants **portability**.

It costs $0.10 per cluster per hour for standard support, or $0.60 on extended support, plus the compute.

### Node types

| Option | Who manages nodes |
| --- | --- |
| **Managed node groups** | EKS creates and manages EC2 nodes in an Auto Scaling group |
| **Self-managed nodes** | You create and register them |
| **Fargate** | No nodes. No DaemonSets or privileged containers, and EFS but not EBS |
| **EKS Auto Mode** | AWS extends management to compute, storage and networking in the cluster |

### Scaling

| Tool | Scales |
| --- | --- |
| **Horizontal Pod Autoscaler** | Number of pods. Needs the Metrics Server |
| **Cluster Autoscaler** | Number of nodes |
| **Karpenter** | Launches well-fitting nodes quickly, in response to demand |

### Storage

EKS uses Container Storage Interface (CSI) drivers. It supports EBS, EFS (including with Fargate), FSx for Lustre and FSx for NetApp ONTAP.

### Security

- IAM authenticates callers to the cluster, and Kubernetes role-based access control authorises them.
- **Access entries** are the recommended way to map IAM principals to Kubernetes permissions.
- **IAM Roles for Service Accounts (IRSA)** and **EKS Pod Identity** give pods their own IAM permissions.

### Running Kubernetes elsewhere

| Option | What it is |
| --- | --- |
| **EKS Anywhere** | Create and operate Kubernetes on your own infrastructure |
| **EKS Distro** | The Kubernetes distribution used by EKS, to run yourself without AWS management |
| **EKS Connector** | View outside clusters in the EKS console |

## AWS App Runner

**App Runner** deployed web apps from code or an image, with no infrastructure experience. It has been closed to new customers since 31 March 2026, and AWS recommends ECS Express Mode. It is not on the in-scope list.

## Exam patterns

| If the question says | Think | Why |
| --- | --- | --- |
| Containers with no servers to manage | Fargate | |
| Already runs Kubernetes on-premises | EKS | Minimal change |
| Avoid lock-in, portable across clouds | EKS | |
| Task cannot pull its image from ECR | Task execution role | Launch plumbing |
| App gets AccessDenied calling DynamoDB | Task role | App permissions |
| GPU containers | ECS or EKS on EC2 | No GPUs on Fargate |
| Scan images for vulnerabilities | ECR image scanning | |
| A security group per task | awsvpc mode | |
| Cheap interruptible container jobs | Fargate Spot | |
| Scale tasks on queue length | ECS Service Auto Scaling on queue depth | |
| Shared files between tasks across AZs | EFS | |
| Run ECS on your own servers | ECS Anywhere | |
| Run EKS on your own servers | EKS Anywhere | |
| Run a task when a file arrives | EventBridge to ECS task | |
| Nodes launch quickly with well-fitted sizes | Karpenter | |
| Pods need their own AWS permissions | IRSA or Pod Identity | |

## Check yourself

**1.** A company wants to run containers without managing any EC2 instances, and it has no Kubernetes experience. What is the simplest option?

- A. ECS on Fargate
- B. EKS on self-managed nodes
- C. EC2 with Docker installed
- D. Lambda

> [!success]- Answer
> **A.** ECS is simple and Fargate removes host management.

**2.** A company runs Kubernetes on-premises and wants to move to AWS with minimal changes. What should it use?

- A. ECS
- B. EKS
- C. Elastic Beanstalk
- D. App Runner

> [!success]- Answer
> **B.** EKS is managed Kubernetes, so existing manifests and tools carry over.

**3.** An ECS task starts, but the application receives AccessDenied when it writes to DynamoDB. What should be changed?

- A. The task execution role
- B. The task role
- C. The EC2 instance profile
- D. The ECR repository policy

> [!success]- Answer
> **B.** The task role provides permissions for application code.

**4.** ECS tasks fail to start with an error pulling the image from ECR. What should be checked first?

- A. The task role
- B. The task execution role
- C. The ALB listener
- D. The Route 53 record

> [!success]- Answer
> **B.** ECS uses the execution role to pull images and write logs.

**5.** A company wants to run GPU-based ML inference in containers, with as little management as possible. Which option is appropriate?

- A. ECS on Fargate
- B. ECS on EC2 GPU instances
- C. Lambda
- D. Fargate Spot

> [!success]- Answer
> **B.** Fargate does not support GPUs.

**6.** Fargate tasks in several AZs must share files persistently. Which storage fits?

- A. EBS gp3
- B. Amazon EFS
- C. Instance store
- D. S3 Glacier

> [!success]- Answer
> **B.** EFS can be mounted by tasks across AZs, and it works with Fargate.

**7.** A company wants to reduce the cost of fault-tolerant containerised batch jobs on ECS. Which option helps most?

- A. Fargate Spot
- B. Dedicated Hosts
- C. A larger task size
- D. Provisioned concurrency

> [!success]- Answer
> **A.** Interruptible work suits Fargate Spot, which is discounted compared with regular Fargate.

**8.** Each ECS task needs its own security group. What configuration provides this?

- A. Bridge network mode
- B. awsvpc network mode
- C. Host network mode
- D. A second load balancer

> [!success]- Answer
> **B.** In awsvpc mode each task gets its own network interface, and so its own security group.

---
**Previous:** [[17 API Gateway and Front-End Services]] · **Next:** [[19 Other Compute Services]] · **Plan:** [[Study Guide]]
