---
tags: [service, cat/security, scope/in]
aliases: ["IAM users", "IAM groups", "IAM Roles", "IAM role", "root account"]
---

# IAM Users Groups and Roles

**Root Account** - created by default, shouldn’t be used or shared.

**[[AWS IAM|IAM]] Users** - people within our organization and they can be grouped. Users don't have to belong to a group and one user can belong to multiple groups. Each user has a unique name and credentials (password or [[AWS Access Methods|access keys]]).

**IAM Groups** - collections of users. Instead of attaching policies to individual users, we can assign permissions to groups, making it easier to manage access based on job function or role.

Users or Groups can be assigned JSON documents called **policies** which define the permissions of the user. In AWS we apply the **[[Least Privilege|least privilege]] principle** (don't give more permissions than a user needs).

There are also **IAM Roles** which give permissions to AWS services. Unlike a user, a role doesn’t have long-term credentials. Instead, it can be assumed temporarily by trusted entities.

Cross-account access using IAM roles in AWS allows one AWS account to grant permissions to users or services in another AWS account.

## Exam tasks
- [[Task 1.1 Design secure access to AWS resources]]

---
**Up:** [[AWS IAM]] · **Map:** [[Security Identity and Compliance Map]]
