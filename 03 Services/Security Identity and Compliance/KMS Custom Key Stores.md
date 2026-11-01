---
tags: [service, cat/security, scope/in]
aliases: ["XKS", "External Key Store"]
---

# KMS Custom Key Stores

- **[[AWS KMS|KMS]] - [[AWS CloudHSM|CloudHSM]] Integration.**

    The KMS custom key store feature combines the controls provided by AWS CloudHSM. We can configure our own CloudHSM cluster and authorize KMS to use it as a dedicated key store for our keys rather than the default AWS KMS key store. This is suitable if we want to be able to audit the usage of all our keys independently of KMS or [[AWS CloudTrail|CloudTrail]].

**External Key Store (XKS)** in KMS is a setup where encryption keys are stored and managed outside the primary KMS infrastructure. It enhances security and compliance by allowing organizations to retain control over their encryption keys in a dedicated external system.

**XKS Proxy** is an intermediary service that acts as a bridge, enabling secure key retrieval and management without requiring direct integration with the external key store itself.

## Exam tasks
- [[Task 1.3 Determine appropriate data security controls]]

---
**Up:** [[AWS KMS]] · **Map:** [[Security Identity and Compliance Map]]
