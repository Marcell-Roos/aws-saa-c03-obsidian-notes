---
tags: [service, cat/networking, scope/in]
aliases: ["signed cookies", "Signed URLs"]
---

# CloudFront Signed URLs and Cookies

**[[Amazon CloudFront|CloudFront]] Access Control**

CloudFront signed URLs and signed cookies allow us to control who can access our content.

**Signed URLs** use cases:

- Restrict access to individual files (e.g. an installation download for your application).
- Users are using a client that doesn't support cookies.

**Signed Cookies** use cases:

- Provide access to multiple restricted files (e.g. all of the files for a video in HLS format or all of the files in the subscribers' area of a website).
- We don't want to change our current URLs.

---
**Up:** [[Amazon CloudFront]] · **Map:** [[Networking and Content Delivery Map]]
