---
tags: [concept, scope/in]
aliases: ["envelope encryption"]
---

# Envelope Encryption

A data key encrypts the data, and a [[AWS KMS|KMS key]] encrypts the data key. Only the encrypted data key is stored next to the data.

```mermaid
flowchart LR
    K["KMS key"] -- GenerateDataKey --> P["Plaintext data key"]
    K --> E["Encrypted data key"]
    P --> C["Encrypt data locally"]
    C --> S["Store ciphertext + encrypted data key"]
    E --> S
```

This keeps KMS calls low and lets large data be encrypted locally. An [[S3 Encryption|S3 Bucket Key]] reduces KMS calls further.

## Exam tasks
- [[Task 1.3 Determine appropriate data security controls]]

---
**Up:** [[AWS KMS]]
