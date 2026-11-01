---
tags: [service, cat/storage, scope/in]
---

# S3 Object Lambda

> [!warning] Closed to new customers
> In maintenance since 7 November 2025. AWS suggests alternatives such as Lambda invoked another way or a CloudFront image transformation solution.

We can use [[AWS Lambda]] Functions to change the object before it is retrieved by the caller application. Only one [[Amazon S3|S3 bucket]] is needed, on top of which we create S3 Access Point and S3 Object Lambda [[S3 Access Points|Access Points]].

Use cases:

- Redacting PII information from analytics or non-productiuon environments.
- Converting across data formats, such as converting XML to JSON.
- Resizing and watermarking images on the fly using caller-specific details, such as the user who requested the object.

---
**Up:** [[Amazon S3]] · **Map:** [[Storage Map]]
