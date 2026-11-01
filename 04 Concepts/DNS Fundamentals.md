---
tags: [concept, scope/in]
aliases: ["DNS"]
---

# DNS Fundamentals

**DNS Terminologies**

- Domain Registrar - [[Amazon Route 53|Route 53]], GoDaddy, etc…
- DNS Records - A, AAAA, CNAME, NS, etc…
- Zone File - contains DNS records.
- Name Server - resolves DNS queries (authoritative or non-autorithative).
- Top Level Domain (TLD) - .com, .us, .gov, .org …
- Second Level Domain (SLD) - amazon.com, google.com.

**How DNS Works**

```mermaid
sequenceDiagram
    participant B as Browser
    participant R as Local DNS resolver
    participant Root as Root server
    participant T as TLD server
    participant A as Authoritative server
    B->>R: example.com?
    R->>Root: example.com?
    Root-->>R: Ask the .com TLD
    R->>T: example.com?
    T-->>R: Ask the name servers
    R->>A: example.com?
    A-->>R: 12.34.56.78
    R-->>B: 12.34.56.78, cached for the TTL
```

---
**Up:** [[Amazon Route 53]]
