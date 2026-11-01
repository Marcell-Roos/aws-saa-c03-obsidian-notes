---
tags: [service, cat/security, scope/in]
---

# Amazon Inspector

**Amazon Inspector** is a security assessment service that helps improve the security and compliance of applications deployed on AWS. Inspector automatically assesses applications for vulnerabilities or deviations from best practices (CVE).

Can be used for:

- [[Amazon EC2|EC2 Instances]]
    - Leveraging the [[AWS Systems Manager|SSM]] agent.
    - Analyze against unintended network accessibility.
    - Analyze the running OS against known vulnerabilities.
- Container images push to [[Amazon ECR]]
    - Assessment of container images as they are pushed.
- [[AWS Lambda|Lambda functions]]
    - Identifies software vulnerabilities in function code and package dependencies.
    - Assessment of functions as they are deployed.

Can be integrated with [[AWS Security Hub]] and send findings to [[Amazon EventBridge|EventBridge]].

Amazon Inspector Classic shut down on 20 May 2026, so everything here refers to the current version.

## Exam tasks
- [[Task 1.2 Design secure workloads and applications]]

---
**Map:** [[Security Identity and Compliance Map]]
