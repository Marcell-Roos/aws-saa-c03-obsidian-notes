---
tags: [comparison, scope/in]
---

# CloudFront vs Global Accelerator

Adapted from devesh-talreja's cheat sheet (MIT).

| | [[Amazon CloudFront]] | [[AWS Global Accelerator]] |
| --- | --- | --- |
| Purpose | CDN that caches content | Routes traffic over the AWS backbone |
| Caching | Yes | No |
| Protocols | HTTP, HTTPS, WebSocket | TCP and UDP |
| IPs | Change, so use the domain name | 2 static anycast IPs |
| Best for | Web, media, static assets | Gaming, VoIP, IoT, fast Regional failover |
| Keywords | Cache, CDN, reduce origin load | Static IP, non-HTTP, global failover |

## Exam tasks
- [[Task 3.4 Determine high-performing and or or scalable network architectures]]

---
**Up:** [[Comparisons Map]]
