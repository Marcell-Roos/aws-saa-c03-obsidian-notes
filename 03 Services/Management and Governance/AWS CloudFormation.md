---
tags: [service, cat/management, scope/in]
aliases: ["CloudFormation", "StackSets"]
---

# AWS CloudFormation

**CloudFormation** is a declarative way of outlining our AWS Infrastructure, for any resources.

> Example: We want [[Security Groups|security group]], two [[Amazon EC2|EC2 instances]] using that security group, an [[Amazon S3|S3 bucket]] and [[Elastic Load Balancing|ELB]] in front of these machines. CloudFormation creates all those for us, in the right order, with exact configuration that we specify.

Benefits of CloudFormation

- Infrastructure as code - No resources are manually created, which is excellent for control. Changes to the infrastructure are reviewed through code.
- Cost - Each resources within stack is tagged with an identifier so we can easily see how much a stack costs us. We can estimate the costs of our resources using the CloudFormation template.
- Productivity - Ability to destroy and re-create an infrastructure on the cloud on the fly. We can automate generation of diagrams for our templates.

**AWS Infrastructure Composer** (formerly Application Composer; end of support 29 September 2027) - A visual tool designed to simplify the process of building serverless applications on AWS. It enables developers to drag and drop various AWS services to create an architecture diagram that represents their application.

- **Stacks** are the core unit of deployment in CloudFormation. A stack is a collection of AWS resources that we can manage as a single unit. When you create, update, or delete a stack, CloudFormation automatically provisions or deletes the associated resources in a predictable way.
- **Template** is a JSON or YAML formatted text file that describes the resources AWS CloudFormation will provision in our stack.
- **StackSets** extend the functionality of stacks by allowing us to manage stacks across multiple accounts and regions.

**CloudFormation Service Role** - [[IAM Users Groups and Roles|IAM role]] that allows CloudFormation to create/update/delete stack resources on our behalf. It is useful if we want to achieve the [[Least Privilege|least privilege]] principle, but we don't want to give the user all the required permissions to create the stack resource. User must have iam:PassRole permissions.

## In this topic
- [[CloudFormation Policy Attributes]]

## Exam tasks
- [[Task 2.2 Design highly available and or or fault-tolerant architectures]]

---
**Map:** [[Management and Governance Map]]
