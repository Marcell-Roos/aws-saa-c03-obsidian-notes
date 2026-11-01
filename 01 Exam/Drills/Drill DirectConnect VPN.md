---
tags: [drill, scope/in]
---

# Drill DirectConnect VPN

Adapted from [RonitSachdev/aws-saa-c03-guides](https://github.com/RonitSachdev/aws-saa-c03-guides) (CC BY 4.0), with outdated facts changed.

## Question patterns

- *"Transferring 5 TB nightly; VPN performance is inconsistent"* → **[[AWS Direct Connect|Direct Connect]]** (dedicated fiber = consistent throughput for big regular transfers)
- *"Cost-effective backup for an existing Direct Connect link"* → **[[AWS Site-to-Site VPN|Site-to-Site VPN]] failover** ("cost-effective backup" is the VPN's middle name)
- *"Data over Direct Connect must be encrypted in transit"* → **Site-to-Site VPN over the DX connection** (DX is private, not encrypted)
- *"Must connect on-premises to AWS within days"* → **Site-to-Site VPN** (DX takes weeks–months; VPN takes hours)
- *"Remote employees' laptops need secure access to the [[Amazon VPC|VPC]]"* → **[[AWS Client VPN]]** (individual devices, not a site)
- *"One Direct Connect must reach VPCs in multiple regions"* → **Direct Connect Gateway** (one fiber, many VPCs/regions)
- *"On-prem must reach AWS with no traffic on the public internet"* → **Direct Connect** (the only option that skips the internet entirely)

## Pocket card

| Keyword | Answer |
|---|---|
| Encrypted tunnel, quick, cheap | Site-to-Site VPN |
| VGW + CGW | Site-to-Site VPN components (AWS + customer side) |
| Consistent bandwidth, dedicated | Direct Connect |
| Setup in hours | VPN |
| Setup in weeks–months | Direct Connect |
| Encrypt Direct Connect | VPN over DX |
| Cost-effective DX backup | Site-to-Site VPN |
| One DX → many VPCs/regions | Direct Connect Gateway |
| Remote workers → VPC | Client VPN |
| Private VIF / Public VIF / Transit VIF | VPC / public services / [[AWS Transit Gateway\|Transit Gateway]] |

---
**Up:** [[Drills Map]]
