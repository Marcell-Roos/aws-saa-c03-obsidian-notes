---
tags: [service, cat/compute, scope/in]
aliases: ["Wavelength"]
---

# AWS Wavelength

**AWS Wavelength** is a service that brings AWS compute and storage services to the edge of the 5G network. It enables developers to build ultra-low-latency applications by deploying them closer to end-users, specifically within the infrastructure of telecom providers.

**Wavelength Zones** are specific infrastructure deployments that host AWS compute and storage services within the 5G networks. These zones are deployed in partnership with telecom providers like Verizon, Vodafone, KDDI, and SK Telecom, among others. We can extend our [[Amazon VPC|VPC]] into Wavelength Zones.

**Carrier Gateway** - networking component used specifically in Wavelength Zones to enable communication between our VPC and devices connected to 5G networks. It provides a route for traffic between your VPC and the telecom provider's 5G network, allowing your Wavelength-hosted applications to communicate with devices using carrier-assigned IP addresses.

Communication between applications and 5G devices can remain private within the telecom provider's network without ever needing to cross the public internet.

---
**Up:** [[AWS Hybrid and Edge Compute]] · **Map:** [[Compute Map]]
