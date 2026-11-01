---
tags: [service, cat/networking, scope/in]
aliases: ["Deregistration Delay", "connection draining"]
---

# ELB Deregistration Delay

**Deregistration Delay** ensures that in-flight requests are handled properly when instances are deregistered or terminated. It stops sending new requests to the [[Amazon EC2|EC2 instance]] which is de-registering.

We can set timeout between 1 to 3600s (default is 300s). It can be disabled if we se value to 0. Good practice is to set to a low value if our requests are short.

---
**Up:** [[Elastic Load Balancing]] · **Map:** [[Networking and Content Delivery Map]]
