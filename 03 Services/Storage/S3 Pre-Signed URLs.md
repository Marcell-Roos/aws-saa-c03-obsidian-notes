---
tags: [service, cat/storage, scope/in]
aliases: ["pre-signed URL", "pre-signed URLs", "presigned URL"]
---

# S3 Pre-Signed URLs

We can generate pre-signed URLs using the [[Amazon S3|S3]] Console, [[AWS CLI]] or SDK. Users given a pre-signed URL inherit the permissions of the user that generated the URL for GET and PUT methods.

Use cases:

- Allow only logged-in users to download a premium video from our S3 bucket.
- Allow an ever-changing list of users to download files by generating URLs dynamically.
- Allow temporarily a user to upload a file to a precise location in our S3 bucket.

Pre-signed URLs **allow users to interact directly with the cloud storage service rather than routing through our application server**. This can reduce latency.

The URL carries the permissions of the identity that signed it, checked at request time. It expires after a set time.

---
**Up:** [[Amazon S3]] · **Map:** [[Storage Map]]
