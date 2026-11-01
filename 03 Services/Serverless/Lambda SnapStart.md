---
tags: [service, cat/serverless, scope/in]
aliases: ["SnapStart"]
---

# Lambda SnapStart

**Lambda SnapStart** improves startup performance by up to 10x. It supports Java 11+ (no extra cost) plus Python 3.12+ and .NET 8+ (which are charged for snapshot caching and restoration). When enabled, function is invoked from a preinitialized state (no function initialization from scratch).

When we publish a new version, [[AWS Lambda|Lambda]] initializes our function, takes a snapshot of memory and disk state of the initialized function and then snapshot is cached for low-latency access.

---
**Up:** [[AWS Lambda]] · **Map:** [[Serverless Map]]
