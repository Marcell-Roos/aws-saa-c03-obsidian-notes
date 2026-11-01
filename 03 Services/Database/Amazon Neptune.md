---
tags: [service, cat/database, scope/in]
aliases: ["Neptune"]
---

# Amazon Neptune

**Neptune** is a fully managed graph database. It is highly available across 3 AZ, with up to 15 [[RDS Read Replicas|Read Replicas]]. We can build and run apps working with highly connected datasets (optimized for these complex and hard queries). It can store up to billions of relations and query the graph with milliseconds latency.

**Neptune Streams** - real-time ordered sequence of every change to our graph data. Changes are available immediately after writing. There are no duplicates and order is strict. Streams data is accessible in an HTTP REST API.

Use cases: send notifications when certain changes are made, maintain our graph data synchronized in another data store, replicate data across regions in Neptune.

## Exam tasks
- [[Task 3.3 Determine high-performing database solutions]]

---
**Up:** [[Purpose-Built Databases]] · **Map:** [[Database Map]]
