---
tags: [service, cat/storage, scope/in]
aliases: ["MFA Delete"]
---

# S3 MFA Delete

**MFA Delete** is a feature designed to add an extra layer of security to protect our [[Amazon S3|S3 bucket]]'s objects from accidental or malicious deletion. It requires users to provide two or more forms of verification before they can perform deletion.

To use MFA Delete, Versioning must be enabled on the bucket and only the bucket owner ([[IAM Users Groups and Roles|root account]]) can enable/disable MFA Delete.

---
**Up:** [[Amazon S3]] · **Map:** [[Storage Map]]
