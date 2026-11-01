---
tags: [service, cat/management, scope/in]
aliases: ["Systems Manager", "SSM"]
---

# AWS Systems Manager

**SSM** is a hybrid service that helps us manage our [[Amazon EC2|EC2]] and On-Premises systems at scale. We can get operational insights about the state of our infrastructure.

Most important features of SSM:

- Patching automation for enhanced compliance.
- Run commands across an entire fleet of servers.
- Store parameter configuration with the [[SSM Parameter Store]].

We need to install the SSM agent onto the systems we control (installed by default on Amazon Linux [[Amazon Machine Image|AMI]]). If an instance can't be controlled with SSM, it’s probably an issue with the SSM agent. With SSM agent we can run commands, patch and configure our servers.

## In this topic
- [[SSM Automation]]
- [[SSM Maintenance Windows]]
- [[SSM Parameter Store]]
- [[SSM Patch Manager]]
- [[SSM Run Command]]
- [[SSM Session Manager]]
- [[SSM State Manager and Fleet Manager]]

---
**Map:** [[Management and Governance Map]]
