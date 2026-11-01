---
tags: [service, cat/networking, scope/in]
aliases: ["Geolocation"]
---

# Route 53 Geolocation Routing

It allows us to route traffic to different resources based on the geographic location of our users. This feature is useful for delivering content or services that are tailored to specific regions, optimizing performance, and improving the user experience (website localization, restrict content distributions).

We should create a “Default” record (in case there is no match on location). Also, it can be associated with [[Route 53 Health Checks|Health Checks]].

---
**Up:** [[Route 53 Routing Policies]] · **Map:** [[Networking and Content Delivery Map]]
