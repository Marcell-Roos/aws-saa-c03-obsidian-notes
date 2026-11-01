---
tags: [service, cat/networking, scope/in]
aliases: ["Weighted Routing"]
---

# Route 53 Weighted Routing

It controls the percentage of the requests that go to each specific resource.

$$
traffic = \frac{weight\ for\ a\ specific\ record}{sum\ of\ all\ the\ weights\ for\ all\ records}
$$

[[DNS Fundamentals|DNS]] records must have the same name and type. This [[Route 53 Routing Policies|routing policy]] can be associated with [[Route 53 Health Checks|Health Checks]].

- **Assign a weight 0 to a record to stop sending traffic to a resource.**
- **If all records have weight of 0, then all records will be returned equally.**

Use cases: load balancing between regions, testing new application versions …

---
**Up:** [[Route 53 Routing Policies]] · **Map:** [[Networking and Content Delivery Map]]
