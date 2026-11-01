---
tags: [comparison, scope/in]
---

# ALB vs NLB vs GWLB

| | [[Application Load Balancer]] | [[Network Load Balancer]] | [[Gateway Load Balancer]] |
| --- | --- | --- | --- |
| Layer | 7 | 4 | 3 |
| Protocols | HTTP, HTTPS, gRPC, WebSocket | TCP, UDP, TLS, QUIC | IP, using GENEVE on 6081 |
| Routing | Path, host, header, query | Listener and port | Flows to appliances |
| Static IP | No | Yes, one per AZ, Elastic IP allowed | No |
| Targets | Instances, IPs, [[AWS Lambda\|Lambda]], containers | Instances, IPs, [[Application Load Balancer\|ALB]] | Instances, IPs |
| Security groups | Yes | Yes | No |
| Use for | Web apps, microservices | Extreme performance, static IP, [[AWS PrivateLink\|PrivateLink]] | Firewalls and inspection |

Questions can also compare them on cost: choose the simplest [[Elastic Load Balancing|load balancer]] that meets the protocol need.

## Exam tasks
- [[Task 3.4 Determine high-performing and or or scalable network architectures]]
- [[Task 4.2 Design cost-optimized compute solutions]]

---
**Up:** [[Comparisons Map]]
