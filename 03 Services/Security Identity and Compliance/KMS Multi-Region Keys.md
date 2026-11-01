---
tags: [service, cat/security, scope/in]
aliases: ["Multi-Region Keys", "MRK"]
---

# KMS Multi-Region Keys

**Multi-Region Keys** are identical [[AWS KMS|KMS keys]] in different regions that can be used interchangeably. They have the sam key ID, key material and automatic rotation. We can encrypt in one region and decrypt in other regions (no need to re-encrypt or make cross-region API calls).

KMS Multi-Region is not global (primary + replicas). Each Multi-Region key is managed independently.

**[[DynamoDB Global Tables]]/Global [[Amazon Aurora|Aurora]] & KMS MRK Client-Side Encryption**

We can encrypt specific attributes client-side in our [[Amazon DynamoDB|DynamoDB]] table using DynamoDB Encryption Client. Combined with Global Tables, the client-side encrypted data is replicated to other regions. If we use a MRK replicated in the same region as the DynamoDB Global table, then clients in these regions can use low-latency API calls to KMS in their region to decrypt the data client-side.

Using client-side encryption we can protect specific fields and guarantee only decryption if the client has access to an API key.

We can encrypt specific attributes client-side in our Aurora table using the AWS Encryption SDK. Combined with [[Aurora Global Database|Aurora Global]] Tables, the client-side encrypted data is replicated to other regions. We can protect specific fields even from database admins.

## Exam tasks
- [[Task 1.3 Determine appropriate data security controls]]

---
**Up:** [[AWS KMS]] · **Map:** [[Security Identity and Compliance Map]]
