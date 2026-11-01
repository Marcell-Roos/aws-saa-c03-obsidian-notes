---
tags: [service, cat/security, scope/in]
aliases: ["access keys", "Access Keys"]
---

# AWS Access Methods

**Access Keys** are credentials used to authenticate and authorize API requests to AWS services. These keys consist of:

1. **Access Key ID**: Unique identifier that AWS uses to identify the [[AWS IAM|IAM]] user or AWS account making the API request.
2. **Secret Access Key**: Secret key known only to the IAM user or AWS account. It is used to digitally sign API requests made by the user, ensuring that the request is authentic and comes from a trusted source.

Three options to access AWS:

- **[[AWS Management Console]]** (Protected by [[IAM Password Policy and MFA|MFA]])

    Web-based interface provided by AWS that allows users to access and manage their AWS services and resources.

- **[[AWS CLI]]** (Protected by access keys)

    A tool that enables interaction with AWS services using commands in command line shell. It lets us to direct access public APIs of AWS services. We can use it to develop script to manage our resources.

- **AWS SDK** (Protected by access keys, out of scope for the exam)

    It consists of libraries that let us to access and manage AWS services programmatically.

Access keys are generated through the AWS Console. Users manage their own access keys.

**AWS CloudShell** is a browser-based shell environment that allows us to manage and interact with AWS resources directly from web browser. It’s not available in all regions. CloudShell is on the exam's out-of-scope list.

---
**Up:** [[AWS IAM]] · **Map:** [[Security Identity and Compliance Map]]
