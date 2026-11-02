---
tags: [exam, scope/in]
aliases: ["Domain 1"]
---

# Domain 1: Design Secure Architectures

**30% of scored content.** The largest domain. It covers who can access what, how networks and applications are protected, and how data is protected. In any question from this domain, prefer least privilege, temporary credentials, private connectivity and encryption.

> [!info] How to use this page
> Each row is an item from AWS's exam guide, word for word. If you can explain the middle column without help, you have covered that item. Follow the link if you cannot.

**Main chapters:** [[02 IAM and Federation|IAM and Federation]] · [[03 Multi-Account Governance|Multi-Account Governance]] · [[07 S3 Security and Data Protection|S3 Security and Data Protection]] · [[09 VPC Fundamentals|VPC Fundamentals]] · [[10 VPC Connectivity and Hybrid Networking|VPC Connectivity and Hybrid Networking]] · [[23 Encryption and Secrets|Encryption and Secrets]] · [[24 Threat Protection and Security Services|Threat Protection and Security Services]]

## Task 1.1

**Design secure access to AWS resources**

Who can do what, in one account and across many. Expect roles, cross-account access, federation and SCPs.

### Knowledge of

| Exam guide item | What you need to know | Where |
| --- | --- | --- |
| Access controls and management across multiple accounts | Use Organizations to group accounts, SCPs and RCPs to set ceilings, and cross-account roles to reach resources. | [[03 Multi-Account Governance\|Multi-Account Governance]], [[02 IAM and Federation#Cross-account access\|Cross-account access]] |
| AWS federated access and identity services (for example, IAM, AWS IAM Identity Center) | IAM roles with temporary credentials, Identity Center for the workforce, Cognito for app customers, SAML and OIDC federation. | [[02 IAM and Federation#Federation\|Federation]], [[02 IAM and Federation#AWS IAM Identity Center\|AWS IAM Identity Center]] |
| AWS global infrastructure (for example, Availability Zones, AWS Regions) | Regions, AZs and edge locations, and how to choose a Region. | [[01 Cloud Foundations#The global infrastructure\|The global infrastructure]] |
| AWS security best practices (for example, the principle of least privilege) | Grant the least access needed, use MFA and roles, and audit with Access Analyzer. | [[02 IAM and Federation#Least privilege\|Least privilege]], [[02 IAM and Federation#Auditing IAM\|Auditing IAM]] |
| The AWS shared responsibility model | AWS secures the cloud. You secure what is in it. The line moves with the service. | [[01 Cloud Foundations#The shared responsibility model\|The shared responsibility model]] |

### Skills in

| Exam guide item | What you need to do | Where |
| --- | --- | --- |
| Applying AWS security best practices to IAM users and root users (for example, multi-factor authentication [MFA]) | MFA on root, no root access keys, password policies, and the few tasks only root can do. | [[02 IAM and Federation#The root user\|The root user]], [[02 IAM and Federation#Passwords and MFA\|Passwords and MFA]] |
| Designing a flexible authorization model that includes IAM users, groups, roles, and policies | When to use users, groups and roles. Policy types and how they are evaluated. | [[02 IAM and Federation#IAM identities\|IAM identities]], [[02 IAM and Federation#Policy evaluation logic\|Policy evaluation logic]] |
| Designing a role-based access control strategy (for example, AWS STS, role switching, cross-account access) | AssumeRole, trust policies, ExternalId, and session lengths. | [[02 IAM and Federation#Roles and temporary credentials\|Roles and temporary credentials]], [[02 IAM and Federation#Cross-account access\|Cross-account access]] |
| Designing a security strategy for multiple AWS accounts (for example, AWS Control Tower, service control policies [SCPs]) | Organizations, OUs, SCPs, Control Tower and its controls. | [[03 Multi-Account Governance#Service control policies\|Service control policies]], [[03 Multi-Account Governance#AWS Control Tower\|AWS Control Tower]] |
| Determining the appropriate use of resource policies for AWS services | Resource-based policies keep the caller's permissions. Roles replace them. | [[02 IAM and Federation#Policy types\|Policy types]], [[02 IAM and Federation#Cross-account access\|Cross-account access]] |
| Determining when to federate a directory service with IAM roles | AD Connector, Managed Microsoft AD and SAML federation through Identity Center. | [[02 IAM and Federation#AWS Directory Service\|AWS Directory Service]], [[02 IAM and Federation#Federation\|Federation]] |

## Task 1.2

**Design secure workloads and applications**

Protect the network and the application. Expect VPC design, firewalls, WAF, Shield and Secrets Manager.

### Knowledge of

| Exam guide item | What you need to know | Where |
| --- | --- | --- |
| Application configuration and credentials security | Never store credentials in code. Use roles, Secrets Manager and Parameter Store. | [[23 Encryption and Secrets#Secrets Manager and Parameter Store\|Secrets Manager and Parameter Store]], [[02 IAM and Federation#Roles and temporary credentials\|Roles and temporary credentials]] |
| AWS service endpoints | Gateway and interface endpoints reach AWS services privately. Endpoint policies limit them. | [[10 VPC Connectivity and Hybrid Networking#VPC endpoints\|VPC endpoints]] |
| Control ports, protocols, and network traffic on AWS | Security groups, NACLs, ephemeral ports and common port numbers. | [[09 VPC Fundamentals#Security groups and network ACLs\|Security groups and network ACLs]], [[09 VPC Fundamentals#Ports to know\|Ports to know]] |
| Secure application access | Cognito, ALB authentication and API Gateway authorisers. | [[02 IAM and Federation#Amazon Cognito\|Amazon Cognito]], [[17 API Gateway and Front-End Services#Security\|Security]] |
| Security services with appropriate use cases (for example, Amazon Cognito, Amazon GuardDuty, Amazon Macie) | Match each security service to its one job. | [[24 Threat Protection and Security Services#Who does what\|Who does what]] |
| Threat vectors external to AWS (for example, DDoS, SQL injection) | DDoS at layers 3, 4 and 7, SQL injection and cross-site scripting. | [[24 Threat Protection and Security Services#DDoS protection in layers\|DDoS protection in layers]], [[24 Threat Protection and Security Services#AWS WAF\|AWS WAF]] |

### Skills in

| Exam guide item | What you need to do | Where |
| --- | --- | --- |
| Designing VPC architectures with security components (for example, security groups, route tables, network ACLs, NAT gateways) | Build the three-tier VPC, including route tables, NAT and firewalls. | [[09 VPC Fundamentals#The big picture\|The big picture]], [[09 VPC Fundamentals#NAT for private subnets\|NAT for private subnets]] |
| Determining network segmentation strategies (for example, using public subnets and private subnets) | Public subnets hold only load balancers and NAT. Applications and data stay private. | [[09 VPC Fundamentals#Subnets\|Subnets]], [[31 Architecture Patterns#Multi-tier architecture\|Multi-tier architecture]] |
| Integrating AWS services to secure applications (for example, AWS Shield, AWS WAF, IAM Identity Center, AWS Secrets Manager) | Combine Shield, WAF, Identity Center and Secrets Manager with your application. | [[24 Threat Protection and Security Services#AWS WAF\|AWS WAF]], [[24 Threat Protection and Security Services#AWS Shield\|AWS Shield]], [[23 Encryption and Secrets#AWS Secrets Manager\|AWS Secrets Manager]] |
| Securing external network connections to and from the AWS Cloud (for example, VPN, AWS Direct Connect) | VPN for encrypted links, Direct Connect for private links, and both together. | [[10 VPC Connectivity and Hybrid Networking#AWS Site-to-Site VPN\|AWS Site-to-Site VPN]], [[10 VPC Connectivity and Hybrid Networking#AWS Direct Connect\|AWS Direct Connect]] |

## Task 1.3

**Determine appropriate data security controls**

Protect the data itself. Expect encryption choices, key policies, S3 Object Lock, backups and rotation.

### Knowledge of

| Exam guide item | What you need to know | Where |
| --- | --- | --- |
| Data access and governance | Control access with bucket policies, Lake Formation and Macie, and watch it with CloudTrail. | [[07 S3 Security and Data Protection#How access is decided\|How access is decided]], [[22 Data Lakes and Analytics#AWS Lake Formation\|AWS Lake Formation]] |
| Data recovery | Versioning, snapshots, AWS Backup and point-in-time recovery. | [[28 High Availability and Disaster Recovery#AWS Backup\|AWS Backup]], [[06 Amazon S3#Versioning\|Versioning]] |
| Data retention and classification | Lifecycle rules, Object Lock retention, and Macie to classify sensitive data. | [[07 S3 Security and Data Protection#S3 Object Lock\|S3 Object Lock]], [[24 Threat Protection and Security Services#Amazon Macie\|Amazon Macie]] |
| Encryption and appropriate key management | KMS key types, envelope encryption, CloudHSM, and when to use each. | [[23 Encryption and Secrets#AWS KMS\|AWS KMS]], [[23 Encryption and Secrets#AWS CloudHSM\|AWS CloudHSM]] |

### Skills in

| Exam guide item | What you need to do | Where |
| --- | --- | --- |
| Aligning AWS technologies to meet compliance requirements | Use Artifact, Config, Object Lock and CloudTrail together. | [[24 Threat Protection and Security Services#Compliance in practice\|Compliance in practice]] |
| Encrypting data at rest (for example, AWS KMS) | Choose between SSE-S3, SSE-KMS, DSSE-KMS, SSE-C and client-side encryption. | [[07 S3 Security and Data Protection#Encryption at rest\|Encryption at rest]], [[23 Encryption and Secrets#AWS KMS\|AWS KMS]] |
| Encrypting data in transit (for example, AWS Certificate Manager [ACM] using TLS) | TLS through ACM, and forcing HTTPS with `aws:SecureTransport`. | [[23 Encryption and Secrets#AWS Certificate Manager\|AWS Certificate Manager]], [[07 S3 Security and Data Protection#Encryption in transit\|Encryption in transit]] |
| Implementing access policies for encryption keys | Key policies must allow access, alongside IAM. Grants and cross-account use. | [[23 Encryption and Secrets#Key policies\|Key policies]] |
| Implementing data backups and replications | AWS Backup, cross-Region copies and S3 replication. | [[28 High Availability and Disaster Recovery#AWS Backup\|AWS Backup]], [[06 Amazon S3#Replication\|Replication]] |
| Implementing policies for data access, lifecycle, and protection | Bucket policies, lifecycle rules, Object Lock and MFA Delete. | [[06 Amazon S3#Lifecycle rules\|Lifecycle rules]], [[07 S3 Security and Data Protection#Protecting against deletion\|Protecting against deletion]] |
| Rotating encryption keys and renewing certificates | KMS automatic and on-demand rotation, and ACM renewal, with imported certificates as the exception. | [[23 Encryption and Secrets#Rotation\|Rotation]], [[23 Encryption and Secrets#Renewal\|Renewal]] |

---
**Next:** [[Domain 2 Design Resilient Architectures]] · **Up:** [[SAA-C03 Exam Overview]]
