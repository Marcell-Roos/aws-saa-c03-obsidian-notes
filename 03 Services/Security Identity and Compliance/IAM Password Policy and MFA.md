---
tags: [service, cat/security, scope/in]
aliases: ["MFA", "multi-factor authentication"]
---

# IAM Password Policy and MFA

In AWS we can set minimum password length, specific character types as requirement, allow [[IAM Users Groups and Roles|IAM users]] to change their passwords after some time and prevent password re-use.

**MFA (Multi Factor Authentication)** = password + security device.

- Virtual MFA (Google Authenticator, Authy)

    Support for multiple tokens on a single device.

- Passkeys and FIDO security keys (YubiKey)

    Support for multiple root and IAM users using a single security key.

- Hardware Key Fob MFA Device (Gemalto)
- Hardware Key Fob MFA Device for AWS GovCloud (SurePassID)

## Exam tasks
- [[Task 1.1 Design secure access to AWS resources]]

---
**Up:** [[AWS IAM]] · **Map:** [[Security Identity and Compliance Map]]
