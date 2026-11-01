---
tags: [drill, scope/in]
---

# Drill S3

Adapted from [RonitSachdev/aws-saa-c03-guides](https://github.com/RonitSachdev/aws-saa-c03-guides) (CC BY 4.0), with outdated facts changed.

## Question patterns

- *"Compliance data accessed about twice a year; auditors must receive it within 10 minutes. Most cost-effective class?"* → **[[S3 Storage Classes|Glacier Flexible Retrieval]]** (Deep Archive can never beat 12 hr; Instant passes but costs more; Flexible Expedited = 1–5 min).
- *"Records retained 7 years, almost never accessed, retrieval within 2 business days is acceptable. Cheapest?"* → **Glacier Deep Archive** (deadline ≥ 12 hr finally lets the cheapest class survive).
- *"Reports are heavily used for 30 days, rarely after 90, must always be retrievable in milliseconds."* → **Lifecycle rule: Standard → Standard-IA at 30 days → Glacier Instant Retrieval at 90** (known pattern → lifecycle; "milliseconds" keeps you in Instant, out of Flexible).
- *"Access patterns are unknown and unpredictable; minimize cost without performance impact."* → **Intelligent-Tiering** ("unknown/unpredictable" is its one and only signal).
- *"Thumbnails can be regenerated from originals at any time; store infrequently accessed copies cheaply."* → **One Zone-IA** ("can be regenerated" = single-AZ risk is acceptable).
- *"Processing artifacts are deleted after 20 days. Cheapest class?"* → **[[Amazon S3|S3]] Standard** (under every minimum duration — IA/Glacier would bill 30–180 days anyway).
- *"Security must audit exactly when each encryption key was used, and control key rotation."* → **[[S3 Encryption|SSE-KMS]]** ("audit key usage" is the [[AWS KMS|KMS]] keyword; add S3 Bucket Key if the question moans about KMS request costs).
- *"Regulatory requirement: data must be impossible to delete for 5 years — even by administrators."* → **[[S3 Object Lock and Glacier Vault Lock|Object Lock]], Compliance mode** ("even administrators" rules out Governance).
- *"Objects must be preserved indefinitely while litigation is pending."* → **Legal Hold** ("lawsuit" + no fixed end date).
- *"Users on every continent upload multi-GB video files to a single S3 bucket; speed up uploads."* → **[[S3 Performance|Transfer Acceleration]] + multipart upload** (global UPLOAD to one bucket; global download would be [[Amazon CloudFront|CloudFront]]).
- *"All objects must be encrypted in transit."* → **Bucket policy denying requests where `aws:SecureTransport` is false** (in transit = HTTPS/TLS, not KMS).
- *"Enable access logging for a bucket — what's the key configuration rule?"* → **Deliver logs to a DIFFERENT bucket** (same bucket = infinite logging loop); query them with **[[Amazon Athena|Athena]]**.
- *"Replication was enabled but existing objects didn't copy over."* → **S3 Batch Replication** ([[S3 Replication|CRR]]/SRR only replicate NEW objects).

## Pocket card

| Keyword | Answer |
|---|---|
| Frequently accessed / hot | S3 Standard |
| Lives < 30 days | Standard (minimum-duration charges kill the rest) |
| Infrequent + instant retrieval | Standard-IA |
| "Can be regenerated / secondary copy" | One Zone-IA |
| "Unknown / unpredictable access" | Intelligent-Tiering |
| Known pattern over time | Lifecycle rule (beats Intelligent-Tiering) |
| Archive + milliseconds retrieval | Glacier Instant Retrieval |
| Archive + minutes-to-hours OK | Glacier Flexible (Expedited 1–5 min / Std 3–5 hr / Bulk 5–12 hr) |
| Cheapest, 12+ hr retrieval OK | Glacier Deep Archive (never faster than 12 hr) |
| Object > 5 GB (or > 100 MB) | Multipart upload (required / recommended) |
| Accidental delete/overwrite protection | Versioning (+ [[S3 MFA Delete\|MFA Delete]] for root-MFA-gated deletes) |
| Copy to another region, DR/compliance | CRR (versioning on both sides) |
| Aggregate logs / copy within region | SRR |
| Replicate EXISTING objects | S3 Batch Replication |
| Default encryption, zero effort | SSE-S3 |
| "Audit key usage" / control rotation | SSE-KMS (in [[AWS CloudTrail\|CloudTrail]]) |
| KMS request costs too high | S3 Bucket Key (~99% fewer KMS calls, coarser audit) |
| Customer supplies key per request | SSE-C (HTTPS mandatory) |
| "AWS must never see plaintext" | Client-side encryption |
| Encrypt in transit / enforce HTTPS | Deny aws:SecureTransport = false |
| Encrypt EXISTING objects | [[S3 Batch Operations]] |
| WORM, "not even root can delete" | Object Lock — Compliance mode |
| WORM, privileged users may bypass | Object Lock — Governance mode |
| "Lawsuit," indefinite hold | Legal Hold |
| Temporary download link, no AWS account | Presigned URL (creator's perms, ≤ 7 days) |
| Public policy exists but access fails | [[S3 Access Control\|Block Public Access]] is on |
| S3 reachable only via CloudFront | [[CloudFront Origins\|OAC]] |
| Who accessed — cheap/complete/delayed | S3 Server Access Logs (different bucket! + Athena) |
| Who accessed — real-time + IAM identity | CloudTrail data events |
| More requests/sec | More prefixes (3,500 PUT / 5,500 GET per prefix) |
| Global UPLOADS to one bucket | Transfer Acceleration (pay only if faster) |
| Global DOWNLOADS | CloudFront |
| Download part of an object | Byte-range fetch |
| "When object uploaded, trigger..." | Event notification → Lambda/SQS/SNS/EventBridge |
| SQL across S3 data | Athena (S3 Select is closed to new customers) |
| SQL across S3 data sets | Athena |

---
**Up:** [[Drills Map]]
