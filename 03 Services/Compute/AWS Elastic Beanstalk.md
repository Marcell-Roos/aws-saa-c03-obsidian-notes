---
tags: [service, cat/compute, scope/in]
aliases: ["Elastic Beanstalk", "Beanstalk"]
---

# AWS Elastic Beanstalk

**Elastic Beanstalk** is a **PaaS** offered by AWS. It is developer-centric view of deploying an application on AWS (**web and non web**). It abstracts much of the infrastructure management, allowing developers to focus on writing code (we still have full control over the configuration) and developing features rather than dealing with the underlying infrastructure. Only the application code is the responsibility of the developer. Can be used for deploying Docker containers.

Beanstalk is free but we need to pay for the underlying instances.

Elastic Beanstalk architecture models:

- **Single Instance deployment** - good for development.
- **LB + [[Amazon EC2 Auto Scaling|ASG]]** - great for production or pre-production web apps.
- **ASG only** - great for non-web apps in production.

**Health Monitoring** - a crucial feature that helps ensure the reliability and availability of our applications. It involves tracking the status of the environment's resources and application instances, detecting issues, and taking appropriate actions to maintain the desired state of the environment. It pushes metrics to [[Amazon CloudWatch|CloudWatch]].

**Elastic Beanstalk Components**

- Application - collection of Elastic Beanstalk components (environments, versions, configurations, …).
- Application Version - an iteration of our application code.
- Environment - collection of AWS resources running an application version (only one application version at a time).

---
**Map:** [[Compute Map]]
