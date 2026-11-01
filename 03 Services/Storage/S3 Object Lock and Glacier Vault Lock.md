---
tags: [service, cat/storage, scope/in]
aliases: ["Object Lock", "Vault Lock", "S3 Object Lock"]
---

# S3 Object Lock and Glacier Vault Lock

**[[Amazon S3 Glacier|S3 Glacier]] Vault Lock** (for legacy Glacier vaults) lets us adopt a WORM (Write Once Read Many) model. We need to create a Vault Lock Policy. It is helpful for compliance and data retention.

**S3 Object Lock** lets us adopt a WORM model and block an object version deletion for a specified amount of time.

- **Retention mode - Compliance**

    Object versions can't be overwritten or deleted by any user, including the root users. Objects retention modes can't be changed and retention periods can't be shortened.

- **Retention mode - Governance**

    Most users can't overwrite or delete an object version or alter its lock settings. Some users have special permissions to change the retention or delete the objects.

**Retention Period** - protect the object for a fixed period, it can be extended.

**Legal Hold** - protect the object indefinitely, independent from retention period.

## Exam tasks
- [[Task 1.3 Determine appropriate data security controls]]

---
**Up:** [[Amazon S3]] · **Map:** [[Storage Map]]
