---
tags: [service, cat/storage, scope/in]
aliases: ["CORS"]
---

# S3 CORS

**CORS** - Web Browser based mechanism to allow requests to other origins while visiting the main origin. The request won't be fulfilled unless the other origin allows for the requests, using CORS Headers (Access-Control-Allow-Origin).

If a client makes a cross-origin request on our [[Amazon S3|S3 bucket]], we need to enable the correct CORS headers. We can allow for a specific origin or * for all origins.

---
**Up:** [[Amazon S3]] · **Map:** [[Storage Map]]
