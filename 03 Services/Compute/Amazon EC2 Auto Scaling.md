---
tags: [service, cat/compute, scope/in]
aliases: ["ASG", "ASGs", "Auto Scaling group", "EC2 Auto Scaling"]
---

# Amazon EC2 Auto Scaling

The goal of **ASG** is to:

- Scale out (add [[Amazon EC2|EC2 instances]]) to match an increased load.
- Scale in (remove EC2 instances) to match a decreased load.
- Ensure we have a minimum and a maximum number of machines running.
- **Automatically register new instances to a [[Elastic Load Balancing|load balancer]].**
- **Replace unhealthy instances**.

When EC2 Auto Scaling responds to a **scale-out** event, it launches one or more instances. These instances start in the **Pending** state. If we added an **autoscaling:EC2_INSTANCE_LAUNCHING** lifecycle hook to our ASG, the instances move from the **Pending** state to the **Pending:Wait** state. After we complete the lifecycle action, the instances enter the **Pending:Proceed** state. When the instances are fully configured, they are attached to the ASG and they enter the **InService** state.

When Amazon EC2 Auto Scaling responds to a **scale-in** event, it terminates one or more instances. These instances are detached from the ASG and enter the **Terminating** state. If we added an **autoscaling:EC2_INSTANCE_TERMINATING** lifecycle hook to our ASG the instances move from the **Terminating** state to the **Terminating:Wait** state. After we complete the lifecycle action, the instances enter the **Terminating:Proceed** state. When the instances are fully terminated, they enter the **Terminated** state.

**ASG Attributes**

- **Launch Template**

    It acts as a blueprint for EC2 instances, allowing us to define a set of configuration parameters that can be reused when we launch new instances. When instances are launched via a launch template, they can automatically be registered with an ELB. A launch template version can't be edited, but we can create a new version and point the ASG at it.

- **Min Size / Max Size / Initial Capacity**
- **[[ASG Scaling Policies|Scaling Policies]]**

It is possible to scale an ASG based on [[Amazon CloudWatch|CloudWatch]] alarms. Based on the alarm we can create scale-out policies or scale-in policies.

**EC2 Termination Policy**

The default policy balances AZs first, then terminates the instance with the oldest launch template or configuration, and then the one closest to the next billing hour.

**Capacity settings:** minimum, maximum and **desired capacity**, which is the number the group tries to keep running.

**Health checks:** EC2 status by default, and ELB health checks can be added so an instance failing at the application level is replaced.

**Lifecycle hooks** pause instances in the wait states described above, so scripts can run during launch or termination.

## In this topic
- [[ASG Scaling Policies]]

## Exam tasks
- [[Task 2.1 Design scalable and loosely coupled architectures]]
- [[Task 3.2 Design high-performing and elastic compute solutions]]

---
**Map:** [[Compute Map]]
