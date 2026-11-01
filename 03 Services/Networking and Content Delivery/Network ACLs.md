---
tags: [service, cat/networking, scope/in]
aliases: ["NACL", "NACLs", "Network ACL"]
---

# Network ACLs

**NACL -** firewall which controls traffic from and to [[Amazon VPC|subnet]]. It can have ALLOW and DENY rules. Rules only include IP addresses. Newly created NACLs will deny everything. We can have one NACL per subnet, new subnets are assigned the Default NACL.

**Default NACL** accepts everything inbound/outbound with the subnets it is associated with. We should not modify the Default NACL, instead we should create custom NACLs.

Rules have a number (1-32766), higher precedence = lower number. First rule match will drive the decision.

**Ephemeral Ports** - temporary, short-lived ports used for outbound connections. They are typically assigned dynamically and used for communication between a client and a server.

- **Client → Web Server:** The client connects to the web server using an ephemeral port.
- **Web Server → Database:** The web server connects to the [[Amazon RDS|RDS]] instance over port 3306 to retrieve or store data.
- **Response from Database → Web Server:** The RDS instance sends responses back to the web server using an ephemeral port.
- **Response from Web Server → Client:** The web server sends the response back to the client.

NACL rules ensure that the web tier can communicate with the database tier while limiting traffic to only the necessary ports. The use of a private subnet for the database ensures it is not directly accessible from the internet, enhancing security.

Ephemeral ports: a [[Stateless and Stateful Workloads|stateless]] NACL must allow return traffic on them, typically 1024 to 65535.

## Exam tasks
- [[Task 1.2 Design secure workloads and applications]]

---
**Up:** [[Amazon VPC]] · **Map:** [[Networking and Content Delivery Map]]
