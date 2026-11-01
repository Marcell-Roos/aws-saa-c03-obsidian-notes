---
tags: [service, cat/storage, scope/in]
aliases: ["SSE-S3", "SSE-KMS", "SSE-C"]
---

# S3 Encryption

- **Server-Side Encryption (SSE)**
    - **SSE with S3-Managed Keys (SSE-S3)** - it is enabled by default and encrypts [[Amazon S3|S3]] objects using keys handled, managed and owned by AWS.

        We must set header *“x-amz-server-side-encryption”:”AES256”*.

    - **SSE with [[AWS KMS|KMS]] Keys stored in AWS KMS (SSE-KMS)** - leverages KMS to manage encryption keys.
    - We must set header *“x-amz-server-side-encryption”:”aws:kms”*.

        If we use SSE-KMS we may be impacted by the KMS limits. When we upload, it calls the GenerateDataKey KMS API and when we download, it calls the Decrypt KMS API.

    - **SSE with Customer-Provided Keys (SSE-C)** - when we want to manage our own encryption keys. Since April 2026 it is blocked by default on new general purpose buckets and must be enabled explicitly.

        We must use HTTPS for this type of encryption. Encryption key must be provided in HTTP headers, for every HTTP request made.

- **Client-Side Encryption**

    This type of encryption leverages client libraries such as S3 Client-Side Encryption Library. Clients must encrypt (decrypt) data themselves before sending (retrieving) to (from) S3. Customer fully manages the keys and encryption cycle.

- **Encryption in Transit**

    S3 exposes two endpoints:

    - HTTP Endpoint (not encrypted)
    - HTTPS Endpoint (encryption in flight)

    HTTPS is mandatory for SSE-C.

    **Force Encryption in Transit**

Use a [[S3 Access Control|bucket policy]] that denies requests where `aws:SecureTransport` is false.

SSE-S3 encryption is automatically applied to new objects stored in S3 buckets. Optionally, we can force encryption using a bucket policy and refuse any API call to PUT an S3 object without encryption headers (SSE-KMS or SSE-C).

Bucket Policies are evaluated before “Default Encryption”.

**DSSE-KMS** applies two layers of encryption. An **S3 Bucket Key** reduces SSE-KMS request costs. To enforce HTTPS, deny requests where `aws:SecureTransport` is false.

## Exam tasks
- [[Task 1.3 Determine appropriate data security controls]]

---
**Up:** [[Amazon S3]] · **Map:** [[Storage Map]]
