---
tags: [drill, scope/in]
---

# Drill VPC

Adapted from [RonitSachdev/aws-saa-c03-guides](https://github.com/RonitSachdev/aws-saa-c03-guides) (CC BY 4.0), with outdated facts changed.

## Question patterns

- *"Block all traffic from a specific IP address"* → **[[Network ACLs|NACL]] deny rule** ([[Security Groups|security groups]] can't deny)
- *"Only the app tier may connect to the database"* → **DB security group allows inbound from the app tier's SG** (SG-to-SG reference)
- *"Private [[Amazon EC2|EC2]] must access [[Amazon S3|S3]] privately at the lowest cost"* → **Gateway [[VPC Endpoints|VPC Endpoint]]** (free — [[NAT Gateways|NAT Gateway]] is the expensive decoy)
- *"25 [[Amazon VPC|VPCs]] plus on-premises via VPN must all communicate"* → **[[AWS Transit Gateway|Transit Gateway]]** (peering mesh = 300 connections; TGW is the hub)
- *"Expose one application to a partner VPC; [[CIDR and IP Addressing|CIDR]] ranges overlap"* → **[[AWS PrivateLink|PrivateLink]]** ([[Network Load Balancer|NLB]] + endpoint service; overlap doesn't matter)
- *"Single NAT Gateway — make the design highly available"* → **One NAT Gateway per AZ**, each private subnet routing to its local one
- *"Private instances need to download OS updates"* → **NAT Gateway in the public subnet** + private route `0.0.0.0/0 → NAT`
- *"Most secure way for admins to access private instances"* → **[[SSM Session Manager]]** (no port 22, no bastion, fully logged)
- *"Determine why traffic to an instance is being rejected"* → **[[VPC Flow Logs]]** (metadata shows ACCEPT/REJECT; full packets = [[VPC Traffic Mirroring|Traffic Mirroring]])
- *"IPv6-only instances need outbound internet, no inbound"* → **Egress-only Internet Gateway** (IPv6's "NAT")
- *"NAT instance stopped forwarding traffic"* → **Disable the source/destination check**
- *"Outbound requests succeed but responses never arrive"* → **NACL missing outbound ephemeral-port (1024–65535) rule** (stateless!)

## Pocket card

| Keyword | Answer |
|---|---|
| Public subnet definition | Route to IGW |
| Outbound-only internet for private subnet | NAT Gateway (in a public subnet) |
| NAT high availability | One NAT Gateway per AZ |
| NAT instance fix | Disable source/dest check |
| IPv6 outbound-only | Egress-only IGW |
| Reserved IPs per subnet | 5 |
| VPC CIDR size | /16 to /28 |
| Block a specific IP | NACL (deny) |
| Stateful / instance-level | Security Group |
| Stateless / subnet-level / ephemeral ports | NACL |
| Tier-to-tier access control | SG referencing another SG |
| S3/DynamoDB private + free | Gateway Endpoint |
| Endpoint reachable from on-prem/peered VPC | Interface Endpoint (PrivateLink) |
| 2–3 VPCs, full access | VPC Peering (not transitive!) |
| Many VPCs + VPN/DX, transitive hub | Transit Gateway (RAM to share, only multicast) |
| One service, overlapping CIDRs, SaaS | PrivateLink (NLB + endpoint service) |
| Traffic metadata, accept/reject | Flow Logs |
| Full packet capture | Traffic Mirroring |
| Most secure admin access | SSM Session Manager |
| One network, many accounts | VPC Sharing via RAM |

---
**Up:** [[Drills Map]]
