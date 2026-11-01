---
tags: [service, cat/compute, scope/in]
aliases: ["Dedicated Hosts", "Dedicated Host", "Dedicated Instances"]
---

# EC2 Dedicated Hosts and Instances

- **Dedicated Instances**: no other customers will share our hardware.

    Instances run on hardware that’s dedicated to us. May share hardware with other instances in same account.

- **Dedicated Hosts**: book an entire physical server, control instance placement.

    A physical server with [[Amazon EC2|EC2 instance]] capacity full dedicated to our use. Allows us to address compliance requirements and use existing server-bound software licenses (per-socket, per- core). This is the most expensive option.

    Useful for software that have complicated licensing model and for companies that have strong regulatory or compliance needs.

    **Purchasing Options**:

    - On-demand: pay per second for active dedicated host.
    - Reserved: 1 or 3 years

---
**Up:** [[EC2 Purchasing Options]] · **Map:** [[Compute Map]]
