---
tags: [service, cat/networking, scope/in]
---

# Route 53 TTL

**TTL** is a mechanism that specifies the duration that [[DNS Fundamentals|DNS]] resolvers should cache the information for a DNS record before querying the authoritative DNS server ([[Amazon Route 53|Route 53]]) for updated information.

**Short TTLs** (e.g., 60 seconds) - for DNS records that may change frequently, such as records for [[Elastic Load Balancing|load balancers]] or failover records. This allows changes to propagate quickly.

**Long TTLs** (e.g., 86400 seconds for 24 hours) - for stable records that rarely change. This reduces the number of DNS queries and can improve performance and reduce costs.

Except for [[CNAME vs Alias Records|Alias records]], TTL is mandatory for each DNS record.

---
**Up:** [[Amazon Route 53]] · **Map:** [[Networking and Content Delivery Map]]
