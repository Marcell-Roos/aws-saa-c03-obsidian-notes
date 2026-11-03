---
tags: [topic, cat/management, scope/in]
aliases: ["AWS CloudFormation", "CloudFormation", "CloudFormation Policy Attributes", "AWS Systems Manager", "Systems Manager", "SSM", "SSM Automation", "SSM Maintenance Windows", "SSM Patch Manager", "SSM Run Command", "SSM Session Manager", "SSM State Manager and Fleet Manager", "AWS Proton", "Deployment Strategies", "Immutable Infrastructure", "Drill CloudFormation"]
---

# Infrastructure as Code and Operations

> [!info] Why this matters
> "Automation strategies to ensure infrastructure integrity" and "immutable infrastructure" are both in [[Domain 2 Design Resilient Architectures#Task 2.2|Task 2.2]]. Systems Manager appears as the secure, low-overhead way to run fleets.
>
> **Study time:** about 2 hours.

## AWS CloudFormation

**CloudFormation** creates AWS resources from a template, in the right order, with the exact configuration you specify. It is free. You pay only for the resources it creates.

Benefits:

- **Infrastructure as code:** changes are reviewed in code, and nothing is created by hand.
- **Repeatability:** identical environments can be created in any Region.
- **Cost:** resources in a stack are tagged, so you can see what a stack costs. Dev stacks can be deleted at night and rebuilt in the morning.
- **Productivity:** infrastructure can be destroyed and recreated on the fly.

| Term | Meaning |
| --- | --- |
| **Template** | A JSON or YAML file describing resources. `Resources` is the only required section |
| **Stack** | The resources created from a template, managed as one unit |
| **Parameters** | Inputs to a template |
| **Mappings** | Fixed lookup tables, such as an AMI per Region |
| **Outputs** | Values to show or to share with other stacks through `Export` and `ImportValue` |
| **Conditions** | Create resources only in some cases |

### Stack features

| Feature | Purpose |
| --- | --- |
| **Change sets** | Preview what an update will do before applying it |
| **StackSets** | Deploy one template to many accounts and Regions |
| **Drift detection** | Find resources changed outside CloudFormation |
| **Nested stacks** | Reuse common components across templates |
| **Stack policy** | Protect resources from updates |
| **Rollback** | On a failed creation, resources are rolled back by default |
| **Service role** | CloudFormation acts with a role, so that users do not need permissions for every resource. Users need `iam:PassRole` |
| **Hooks** | Check resources before they are provisioned |

### Template functions

| Function | Purpose |
| --- | --- |
| `Ref` | Returns a parameter's value or a resource's identifier |
| `Fn::GetAtt` | Returns an attribute of a resource, such as a load balancer's DNS name |
| `Fn::Sub` | Substitutes values into a string |
| `Fn::Join` | Joins values with a delimiter |
| `Fn::FindInMap` | Looks up a value in `Mappings`, such as an AMI per Region |
| `Fn::ImportValue` | Reads a value exported by another stack |
| `Fn::If` | Chooses a value based on a condition |

**Pseudo parameters** such as `AWS::Region` and `AWS::AccountId` make a template portable. Avoid hardcoding AMI IDs or account numbers, or the template will fail elsewhere.

### Secrets in templates

Never put passwords in a template. Use **dynamic references** such as `{{resolve:secretsmanager:MySecret}}` or `{{resolve:ssm:MyParameter}}`, or mark parameters with `NoEcho`.

### Bootstrapping instances

| Helper | Purpose |
| --- | --- |
| **User data** | Runs a script at first boot |
| `cfn-init` | Applies configuration from the template's metadata |
| `cfn-signal` | Tells CloudFormation that configuration has finished, with `CreationPolicy` |
| `cfn-hup` | Detects metadata changes and applies them |

### Custom resources

A **custom resource** runs a Lambda function during stack operations, for things CloudFormation cannot do alone. A classic use is emptying an S3 bucket, because a stack cannot delete a bucket that still holds objects.

### StackSets permissions

With **service-managed** permissions, StackSets uses AWS Organizations and can deploy to new accounts automatically. With **self-managed** permissions, you create the roles yourself.

### AWS SAM

The **AWS Serverless Application Model** is an extension of CloudFormation, with a short syntax for functions, APIs and tables. Templates include `Transform: AWS::Serverless-2016-10-31`. The Serverless Application Repository holds applications built this way.

### Resource attributes

| Attribute | Purpose |
| --- | --- |
| **`DeletionPolicy`** | What happens when a stack is deleted: `Delete`, `Retain` or `Snapshot` |
| **`UpdateReplacePolicy`** | What happens to a resource replaced during an update |
| **`DependsOn`** | Forces creation order |
| **`CreationPolicy`** | Waits for a success signal, for example from `cfn-signal` once an instance has finished configuring |
| **`UpdatePolicy`** | Controls rolling updates, for instance on an Auto Scaling group |

```yaml
Resources:
  ProductionDb:
    Type: AWS::RDS::DBInstance
    DeletionPolicy: Snapshot
    UpdateReplacePolicy: Snapshot
```

**AWS Infrastructure Composer** is a visual tool for designing templates. It reaches end of support on 29 September 2027, and the standalone console ends support on 7 December 2026.

## AWS Systems Manager

**Systems Manager (SSM)** manages EC2 and on-premises servers at scale. Most features need the **SSM agent**, which is installed by default on Amazon Linux and some other AMIs, and an instance role with the right permissions. If an instance cannot be managed, the agent or role is the likely cause.

| Feature | What it does |
| --- | --- |
| **Session Manager** | Secure shell access with no open ports |
| **Run Command** | Run scripts across a fleet with no SSH |
| **Patch Manager** | Automate OS and application patching |
| **Maintenance Windows** | Schedule tasks |
| **Automation** | Runbooks for common tasks, such as restarting instances or creating an AMI |
| **State Manager** | Keep instances in a defined state |
| **Fleet Manager** | A console view for remote management |
| **Parameter Store** | Configuration and secrets. See [[23 Encryption and Secrets#SSM Parameter Store\|Encryption and Secrets]] |

**Hybrid activations** register on-premises servers as managed nodes, so that the same tools work there. **Inventory** collects software details from managed nodes, and **OpsCenter** gathers operational issues in one place.

### Session Manager

**Session Manager** starts a shell on EC2 and on-premises servers through the SSM agent's outbound connection. There is **no need for port 22, bastion hosts or SSH keys**. Access is controlled by IAM, and sessions can be logged to S3 or CloudWatch Logs. This is the most secure admin access answer.

### Run Command

Runs a script or command across many instances, chosen by tag or resource group, with no SSH. It integrates with IAM and CloudTrail, can be triggered by EventBridge, and can send output to S3 or CloudWatch Logs, and notifications to SNS.

### Patch Manager and Maintenance Windows

**Patch Manager** patches EC2 and on-premises servers, on demand or on a schedule, and it reports compliance. A **Maintenance Window** defines a schedule, a duration, a set of instances and a set of tasks.

### Automation

An **Automation runbook** defines actions on instances and other AWS resources. It can be triggered from the console, by EventBridge, in a Maintenance Window, or as an **AWS Config remediation**.

## AWS Proton

**Proton** gave platform teams managed templates for deploying container and serverless apps. It stays on the exam guide's in-scope list, but AWS ended support on 7 October 2026.

## Deployment strategies

| Strategy | How | Downtime | Rollback | Use |
| --- | --- | --- | --- | --- |
| **All at once** | Replace everything together | Likely | Slow | Non-critical apps |
| **Rolling** | Replace in batches | Minimal, with reduced capacity | Moderate | Apps that tolerate a mix of versions for a while |
| **Blue/green** | Two identical environments, then switch traffic | None | **Instant**: switch back | Critical apps needing a quick, reliable rollback |
| **Canary** | A small share of traffic goes to the new version first | None | Quick | Large user bases, early feedback |
| **A/B testing** | Two versions at once, to compare results | None | Quick | UI and feature tests |
| **Shadow** | The new version processes a copy of production traffic, serving no users | None | Not needed | Validating major updates |

On AWS, traffic can be shifted with [[05 Load Balancing and Auto Scaling#Application Load Balancer|ALB weighted target groups]], [[11 Route 53#Weighted|Route 53 weighted routing]], [[17 API Gateway and Front-End Services#Monitoring and deployment|API Gateway canaries]], Lambda aliases and [[19 Other Compute Services#Deployment policies|Elastic Beanstalk policies]].

## Immutable infrastructure

**Immutable infrastructure** means replacing servers rather than changing them.

1. Bake a new AMI or container image.
2. Roll it out with an [[05 Load Balancing and Auto Scaling#Instance refresh|ASG instance refresh]] or a new environment.
3. Roll back by pointing at the old version.

This prevents **configuration drift** and makes deployments repeatable. CloudFormation and EC2 Image Builder support the approach.

## Exam patterns

| If the question says | Think | Why |
| --- | --- | --- |
| See what a template update will do first | Change sets | |
| Deploy to all accounts and Regions | StackSets | |
| Keep the RDS database when the stack is deleted | `DeletionPolicy: Retain` or `Snapshot` | |
| Did anyone change resources by hand? | Drift detection | |
| Protect a critical resource during updates | Stack policy | |
| Reuse a common VPC design | Nested stacks | |
| Wait until an instance has finished configuring | `CreationPolicy` with `cfn-signal` | |
| Least privilege for people deploying stacks | CloudFormation service role | |
| Manage servers with no SSH | Run Command | |
| Patch a fleet on a schedule | Patch Manager and Maintenance Windows | |
| Most secure admin access | Session Manager | |
| Instance does not appear in Systems Manager | Agent or instance role | |
| Instant rollback | Blue/green | |
| Test on a small share of traffic | Canary | |
| Prevent configuration drift | Immutable infrastructure | |

## Check yourself

**1.** Before updating a production stack, the team must see which resources will be replaced. What should it use?

- A. Drift detection
- B. A change set
- C. A stack policy
- D. StackSets

> [!success]- Answer
> **B.** A change set previews the effect of an update without applying it.

**2.** A company must deploy the same IAM roles and Config rules to every account in its organisation, in several Regions. What should it use?

- A. Nested stacks
- B. CloudFormation StackSets
- C. Elastic Beanstalk
- D. Launch templates

> [!success]- Answer
> **B.** StackSets deploy one template across accounts and Regions.

**3.** A stack contains a production database. When the stack is deleted, a final backup must be kept. What should be set?

- A. `DependsOn`
- B. `CreationPolicy`
- C. `DeletionPolicy: Snapshot`
- D. A change set

> [!success]- Answer
> **C.** `Snapshot` takes a final snapshot before the resource is removed.

**4.** Someone changed a security group by hand, and it no longer matches the template. Which feature finds this?

- A. Drift detection
- B. Stack policy
- C. StackSets
- D. Mappings

> [!success]- Answer
> **A.** Drift detection compares the stack's resources with the template.

**5.** Administrators must run a script across 500 instances, without opening SSH. What should they use?

- A. Systems Manager Run Command
- B. Bastion host
- C. EC2 Instance Connect
- D. User data

> [!success]- Answer
> **A.** Run Command uses the SSM agent. User data only runs at launch.

**6.** A company must apply OS patches to EC2 and on-premises servers during a weekly window, and report compliance. What should it use?

- A. AWS Config alone
- B. Patch Manager with a Maintenance Window
- C. Amazon Inspector alone
- D. CloudFormation

> [!success]- Answer
> **B.** Patch Manager patches and reports. Inspector finds vulnerabilities, but it does not patch.

**7.** An application needs a deployment with instant rollback, and the two versions cannot run side by side for users. Which strategy fits?

- A. Rolling
- B. Blue/green
- C. All at once
- D. Canary

> [!success]- Answer
> **B.** Traffic switches all at once between two full environments, and it can switch back immediately.

**8.** An EC2 instance is not listed as a managed node in Systems Manager, although it is running. What is the most likely cause?

- A. It lacks the SSM agent or an instance role with the right permissions
- B. It is in a public subnet
- C. It has an Elastic IP
- D. It uses gp3

> [!success]- Answer
> **A.** Managed nodes need a running agent and permission to talk to Systems Manager.

---
**Previous:** [[25 Monitoring and Auditing]] · **Next:** [[27 Migration and Data Transfer]] · **Plan:** [[Study Guide]]
