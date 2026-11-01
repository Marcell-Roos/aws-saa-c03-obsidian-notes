---
tags: [service, cat/security, scope/in]
aliases: ["KMS", "KMS key", "KMS keys"]
---

# AWS KMS

**AWS KMS (Key Management Service)** is a managed service that allows us to create and manage encryption keys used to encrypt and decrypt our data. It integrates with many other AWS services to simplify the encryption process.

**Keys Types**

- **Symmetric (AES-256 Keys)** - single encryption key that is used to encrypt and decrypt. AWS services that are integrated with KMS use Symmetric CMKs. We never get access to the KMS key unencrypted (must call KMS API to use).
- **Asymmetric (RSA & ECC Key Pairs)** - public (encrypt) and private (decrypt) key pair. Used for encrypt/decrypt or sign/verify operations. The public key is downloadable, but we can't access the private key unencrypted. It is used for encryption outside of AWS by users who can't call the KMS API.

**Types of KMS Keys**

- **Customer Managed Key (CMK)** - created, managed and used by the customer. Optional automatic rotation (every 365 days by default, with a custom period available) plus on-demand rotation. Possibility to bring our own key.
- **AWS Managed Key** - created, managed and used on the customer’s behalf by AWS. Used by AWS services.
- **AWS Owned Key** - collection of CMKs that an AWS service owns and manages to use in multiple accounts. AWS can use those to protect resources in our account (we can't view the keys).

AWS managed keys rotate automatically every year. For customer managed keys rotation is optional (automatic or on-demand). Keys with imported material can't rotate automatically: import new material for on-demand rotation, or rotate manually by creating a new key and moving an alias.

KMS keys are scoped per region. If we want to to move encrypted [[Amazon EBS|EBS volume]] to another region we need to take snapshot of that EBS volume. Then we need to copy snapshot to another region, we neeed to re-encrypt the snapshot using a different KMS key and then we can restore EBS volume from that snapshot.

KMS HSMs are **FIPS 140-3 Security Level 3** validated. See [[KMS vs CloudHSM]] and [[Envelope Encryption]].

## In this topic
- [[KMS Custom Key Stores]]
- [[KMS Key Policies]]
- [[KMS Multi-Region Keys]]
- [[Lambda Environment Variable Encryption]]
- [[Sharing Encrypted AMIs]]

## Exam tasks
- [[Task 1.3 Determine appropriate data security controls]]

---
**Map:** [[Security Identity and Compliance Map]]
