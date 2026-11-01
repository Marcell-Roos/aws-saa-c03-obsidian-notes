---
tags: [drill, scope/in]
---

# Drill Transit Gateway

Adapted from [RonitSachdev/aws-saa-c03-guides](https://github.com/RonitSachdev/aws-saa-c03-guides) (CC BY 4.0), with outdated facts changed.

## Question patterns

- *"25 [[Amazon VPC|VPCs]] and on-premises datacenter need centralized connectivity"* → **[[AWS Transit Gateway|Transit Gateway]]** (hub-and-spoke kills the n(n-1)/2 mesh)
- *"VPC A peers with B, B peers with C, but A can't reach C"* → **Transit Gateway** (peering is non-transitive; TGW routes transitively)
- *"Prod VPCs must not communicate with dev VPCs, but all need on-prem access"* → **TGW with separate [[Internet Gateway and Route Tables|route tables]] per attachment** (segmentation at the hub)
- *"Application requires IP multicast"* → **Transit Gateway** (the only service that supports it)
- *"Just 2 VPCs need to communicate at lowest cost"* → **VPC peering** (free hourly, TGW would be overkill)
- *"Share the network hub across 50 AWS accounts"* → **TGW shared via [[AWS Resource Access Manager|AWS RAM]]**
- *"Connect hub networks in us-east-1 and eu-west-1"* → **TGW peering** (cross-region hub-to-hub)
- *"All inter-VPC traffic must pass through a firewall appliance"* → **TGW with appliance mode** (symmetric flows through the inspection VPC)

## Pocket card

| Keyword | Answer |
|---|---|
| Many VPCs + on-prem, central hub | Transit Gateway |
| Transitive routing | Transit Gateway (peering can't) |
| n(n-1)/2 peering explosion | Transit Gateway |
| Multicast | Transit Gateway (only one) |
| Isolate prod/dev at the hub | TGW route tables |
| Cross-account TGW | Share via AWS RAM |
| Cross-region hubs | TGW peering |
| [[AWS Direct Connect\|DX]] into TGW | Transit VIF |
| Only 2–3 VPCs, cheapest | VPC peering |
| Expose one service, no network merge | [[AWS PrivateLink\|PrivateLink]] (not TGW) |

---
**Up:** [[Drills Map]]
