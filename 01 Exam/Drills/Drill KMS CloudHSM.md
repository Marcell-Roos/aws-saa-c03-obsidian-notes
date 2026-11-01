---
tags: [drill, scope/in]
---

# Drill KMS CloudHSM

Adapted from [RonitSachdev/aws-saa-c03-guides](https://github.com/RonitSachdev/aws-saa-c03-guides) (CC BY 4.0), with outdated facts changed.

## Question patterns

- *"Security team must audit every use of an encryption key."* → **[[AWS KMS|KMS]] + [[AWS CloudTrail|CloudTrail]]** (every key use is logged — KMS's superpower).
- *"Encrypt a 100MB file using KMS."* → **Envelope encryption via GenerateDataKey** (KMS only encrypts ≤4KB directly).
- *"A compromised key must be deleted immediately."* → **Impossible — 7–30 day mandatory waiting period; disable it now instead**.
- *"Compliance requires FIPS 140-2 Level 3 validated modules."* → **[[AWS CloudHSM|CloudHSM]]** (older answer: KMS HSMs are now FIPS 140-3 Level 3 too, so look for single-tenant).
- *"Keys must be inaccessible even to AWS."* → **CloudHSM** (single-tenant, customer-controlled).
- *"Encrypt data in us-east-1, decrypt the same ciphertext in eu-west-1 (DR/global tables)."* → **KMS multi-Region keys**.
- *"Keys must rotate automatically every year under company control."* → **Customer-managed key with auto-rotation enabled**.
- *"KMS request costs exploded from millions of [[Amazon S3|S3]] objects with [[S3 Encryption|SSE-KMS]]."* → **Enable S3 Bucket Key** (fewer KMS calls; accept coarser audit).
- *"User has full [[AWS IAM|IAM]] KMS permissions but still gets AccessDenied on a key."* → **Key policy doesn't allow them — BOTH key policy and IAM must permit**.

## Pocket card

| Keyword | Answer |
|---|---|
| Audit every key use | KMS + CloudTrail |
| Free, AWS-rotated key | AWS-managed key |
| Your policies, $1/mo, yearly rotation | Customer-managed key |
| Encrypt > 4KB | Envelope encryption / GenerateDataKey |
| Delete key now | Impossible — 7–30 day wait (disable instead) |
| Encrypt/decrypt across Regions | Multi-Region keys |
| Cut KMS costs on S3 | S3 Bucket Key |
| Single-tenant HSM, exclusive key control | CloudHSM |
| "AWS cannot see keys" / dedicated hardware | CloudHSM |
| SSL offload / own CA | CloudHSM |
| Access needs key policy AND IAM | Both must allow |

---
**Up:** [[Drills Map]]
