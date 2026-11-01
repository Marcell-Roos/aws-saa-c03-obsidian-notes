---
tags: [service, cat/migration, scope/in]
---

# Transferring Large Datasets

- **Over the internet/Site-to-Site VPN** - ideal for small to moderate data volumes where latency isn’t a significant concern.
- **Over [[AWS Direct Connect|Direct Connect]]** - suitable for transferring large datasets where consistent, high-throughput, and low-latency connectivity is required.
- **Over [[AWS Snow Family|Snowball]]** - ideal when dealing with extremely large datasets or when we have limited or unreliable internet connectivity.
- **For on-going replication/transfers** - [[AWS Site-to-Site VPN|Site-to-Site VPN]]/DX with [[AWS DMS|DMS]] or [[AWS DataSync|DataSync]].

## Exam tasks
- [[Task 4.1 Design cost-optimized storage solutions]]

---
**Map:** [[Migration and Transfer Map]]
