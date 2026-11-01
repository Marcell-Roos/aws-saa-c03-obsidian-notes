---
tags: [service, cat/storage, scope/in]
aliases: ["bucket policy", "bucket policies", "Bucket Policies", "S3 Bucket Policies", "S3 bucket policies", "Block Public Access"]
---

# S3 Access Control

- **User-Based**

    [[AWS IAM|IAM]] Policies - which API calls should be allowed for a specific user from IAM.

- **Resource-Based**
    - Bucket Policies - bucket wide rules from the [[Amazon S3|S3]] console (allows cross account).

    - Object Access Control List (ACL) - finer grain (can be disable).
    - Bucket Access Control List (ACL) - less common (can be disabled).

    An IAM principal can access an S3 object if the user IAM permissions ALLOW it OR the resources policy ALLOWS it AND there is no explicit DENY.

New buckets default to the **Bucket owner enforced** Object Ownership setting: ACLs are disabled and the bucket owner owns every object. If ACLs are re-enabled, an uploader from another account owns the object unless it grants *bucket-owner-full-control*.

There are bucket settings for block public access. These settings were created to prevent company data leaks. If we know our bucket should never be public, we should leave these on (can be set at the account level).

> If we host static website and get 403 forbidden error, then we should check if bucket policy allows public reads.

---
**Up:** [[Amazon S3]] · **Map:** [[Storage Map]]
