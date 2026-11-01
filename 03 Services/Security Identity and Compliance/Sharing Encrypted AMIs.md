---
tags: [service, cat/security, scope/in]
---

# Sharing Encrypted AMIs

- **[[Amazon Machine Image|AMI]] Sharing Process Encrypted via [[AWS KMS|KMS]].**
    1. AMI in source account is encrypted with KMS key from source account.
    2. Must modify the image attribute to add a Launch Permission which corresponds to the specified target AWS account.
    3. Share the KMS keys used to encrypt the snapshot AMI references with the target account.
    4. The [[IAM Users Groups and Roles|IAM role]]/user in the target account must have the permissions to DescribeKey, ReEncrypt, CreateGrant, Decrypt.
    5. When launching an [[Amazon EC2|EC2 instance]] from AMI, optionally the target account can specify a new KMS key in its own account to re-encrypt the volumes.

---
**Up:** [[AWS KMS]] · **Map:** [[Security Identity and Compliance Map]]
