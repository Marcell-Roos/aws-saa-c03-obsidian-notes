---
tags: [concept, scope/in]
aliases: ["Golden AMI"]
---

# Instantiating Applications Quickly

**[[Amazon EC2|EC2 Instances]]**

- Golden AMI - install our applications, OS dependecies, etc… beforehand and launch our EC2 instance from the Golden AMI.
- Bootstrap using User Data - for dynamic configuration.
- Hybrid - mix Golden AMI and User Data ([[AWS Elastic Beanstalk|Elastic Beanstalk]]).

**[[Amazon RDS|RDS]]**

- Restore from a snapshot - the database will have schemas and data ready.

**[[Amazon EBS|EBS]]**

- Restore from a snapshot - the disk will already be formatted and have data.

---
**Up:** [[Amazon EC2]]
