---
tags: [service, cat/networking, scope/in]
---

# Route 53 Simple Routing

It routes traffic to a single resource. It can specify multiple values in the same record. If multiple values are returned, a random one is chosen by the client.

When Alias is enabled, we can specify only one AWS resource. It cannot be associated with [[Route 53 Health Checks|Health Checks]].

---
**Up:** [[Route 53 Routing Policies]] · **Map:** [[Networking and Content Delivery Map]]
