---
tags: [service, cat/networking, scope/in]
aliases: ["Site-to-Site VPN", "VGW", "Virtual Private Gateway", "Customer Gateway"]
---

# AWS Site-to-Site VPN

**Site-to-Site VPN** is used to connect an on-premises VPN to AWS. The connection is automatically encrypted and it goes over the public internet.

To establish Site-to-Site VPN:

- **On-premises** must use a **Customer Gateway (CGW)** - a physical device or software application on the customer's side of the VPN connection. It can be a hardware VPN device, such as a router or firewall, or it can be software-based.
- **AWS** must use a **Virtual Private Gateway (VGW)** - the VPN concentrator on the Amazon side of the VPN connection within the AWS infrastructure. It is a logical entity that represents a VPN gateway capable of handling multiple VPN connections simultaneously.

On-premises should use public internet-routable IP address for its CGW device or if it’s behind a NAT device that is enabled for NAT traversal (NAT-T), it should use the public IP address of the NAT device.

We **must enable Route Propagation for VGW in the [[Internet Gateway and Route Tables|route table]] that is associated with our [[Amazon VPC|subnets]]**.

> If we need to ping our [[Amazon EC2|EC2 instances]] from on-premises, we need to add the ICMP protocol on the inbound of our [[Security Groups|security groups]].

A standard tunnel carries up to 1.25 Gbps. **Large Bandwidth Tunnels** reach 5 Gbps on [[AWS Transit Gateway|Transit Gateway]] or Cloud WAN. Each connection has two tunnels for redundancy.

## In this topic
- [[AWS Client VPN]]
- [[AWS VPN CloudHub]]

## Exam tasks
- [[Task 1.2 Design secure workloads and applications]]
- [[Task 3.4 Determine high-performing and or or scalable network architectures]]
- [[Task 4.4 Design cost-optimized network architectures]]

---
**Map:** [[Networking and Content Delivery Map]]
