---
tags: [service, cat/networking, scope/in]
aliases: ["Geoproximity"]
---

# Route 53 Geoproximity Routing

It route traffic to our resources based on the geographic location of users and resources. We have ability to shift more traffic to resources based on the defined bias. Resources can be AWS resources (specified in aws region) and non-AWS resources (we need to specify latitude and longitude).

To change the size of the geographic region:

- 1≤ Bias ≤ 99 - more traffic to the resource.
- -99 ≤ Bias ≤ -1 - less traffic to the resource.

We can set it on records directly or build it with [[Amazon Route 53|Route 53]] Traffic Flow.

---
**Up:** [[Route 53 Routing Policies]] · **Map:** [[Networking and Content Delivery Map]]
