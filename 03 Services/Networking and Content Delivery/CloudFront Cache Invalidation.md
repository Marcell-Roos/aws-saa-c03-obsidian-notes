---
tags: [service, cat/networking, scope/in]
aliases: ["Cache Invalidation"]
---

# CloudFront Cache Invalidation

The Cache-Control and Expires headers control how long objects stay in the cache. The **Cache-Control max-age** directive lets us specify how long (in seconds) we want an object to remain in the cache before [[Amazon CloudFront|CloudFront]] gets the object again from the origin server. The minimum expiration time CloudFront supports is 0 seconds.

In case we update the back-end origin, CloudFront doesn't know about it and will only get the refreshed content after the TTL has expired. We can force an entire or partial cache refresh by performing a CloudFront Invalidation. We can invalidate all files or special path.

---
**Up:** [[Amazon CloudFront]] · **Map:** [[Networking and Content Delivery Map]]
