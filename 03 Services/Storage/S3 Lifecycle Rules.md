---
tags: [service, cat/storage, scope/in]
aliases: ["Lifecycle Rules", "lifecycle policy", "Lifecycle Policy", "lifecycle rule", "S3 Analytics"]
---

# S3 Lifecycle Rules

**Lifecycle Rules** in [[Amazon S3|S3]] are a set of actions that we can configure to manage the lifecycle of objects in our bucket. These rules enable us to automatically transition objects to different storage classes or delete them after a specified period. Lifecycle rules help us reduce costs and simplify storage management.

**Transition Actions** - used to configure objects to transition to another storage class.

**Expiration Actions** - used to configure objects to expire (delete) after some time.

- Can be used to delete old versions of files (if versioning is enabled).
- Can be used to delete incomplete Multi-Part uploads.

Rules can be created for a certain prefix or for certain objects tags.

- **Lifecycle Rules Question- Scenario I**

    Our application on [[Amazon EC2|EC2]] creates images thumbnails after profile photos are uploaded to S3. These thumbnails can be easily recreated and only need to be kept for 60 days. The source images should be able to be immediately retrieved for these 60 days, and afterwards, the user can wait up to 6 hours. How to design this?

    - S3 source images can be on **Standard** with a lifecycle configuration to transition them to Glacier after 60 days.
    - S3 thumbnails can be on **One-Zone IA** with a lifecycle configuration to expire them after 60 days.
- **Lifecycle Rules Question- Scenario II**

    A rule in our company states that we should be able to recover our deleted S3 objects immediately for 30 days, although this may happen rarely. After this time, and for up to 365 days, deleted objects should be recoverable within 48 hours.

    - Enable [[S3 Versioning]] in order to have objects version.
    - Transition the “noncurrent versions” of the object to Standard IA.
    - Transition afterwards the “noncurrent versions” to [[S3 Storage Classes|Glacier Deep Archive]].

**S3 Analytics** - helps us decide when to transition objects to the right storage class. Recommendations are only for Standard and Standard IA. Report is updated daily and we need to wait 24 to 48 hours to start seeing data analysis.

## Exam tasks
- [[Task 1.3 Determine appropriate data security controls]]
- [[Task 4.1 Design cost-optimized storage solutions]]

---
**Up:** [[Amazon S3]] · **Map:** [[Storage Map]]
