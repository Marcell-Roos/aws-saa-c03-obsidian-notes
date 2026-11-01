---
tags: [service, cat/networking, scope/in]
aliases: ["Route 53", "Route53", "hosted zone", "Hosted Zone"]
---

# Amazon Route 53

**Route 53** is a highly available, scalable, fully managed and authoritative (we can update the [[DNS Fundamentals|DNS]] records) DNS. It is also a **Domain Registrar** and we have ability to check the health of our resources.

**Records** define how we want to route traffic for a domain. Route 53 supports the following DNS record types: **A, AAAA, CNAME, NS**, CAA, DS, MX, NAPTR, PTR, SOA, TXT, SPF, SRV.

Each record contains:

- **Domain/subdomain Name** (e.g. example.com)
- **Record Type** (e.g. A, AAAA)
- **Value** (e.g. 12.34.56.78)
- **[[Route 53 Routing Policies|Routing Policy]]** - how Route 53 responds to queries.
- **TTL (Time to Live)** - amount of time the record is cached at DNS Resolvers.

**Record Types**

- A - maps a domain name to an IPv4 address.
- AAAA - maps a domain name to an [[IPv6 in a VPC|IPv6]] address.
- CNAME - maps hostname to another hostname. The target is a domain name which must have an A or AAAA record. We can't create a [[CNAME vs Alias Records|CNAME record]] for the top node of DNS namespace (Zone Apex).
- NS - specifies the authoritative DNS servers for the domain. For example, *example.com* might have NS records pointing to *ns1.example.com* and *ns2.example.com*.
- MX - specifies the mail server responsible for receiving emails for the domain.

**Hosted Zones** - a container for records that define how to route traffic to a domain and its subdomains. We pay $0.50 per month per hosted zone (for the first 25 zones).

- **Public Hosted Zones** - contain records that specify how to route traffic on the internet.

- **Private Hosted Zones** - contain records that specify how we route traffic within one or more [[Amazon VPC|VPCs]].

- **Routing Traffic to a Website Hosted in [[Amazon S3|S3]].**

    The S3 bucket must have the same name as our domain or subdomain. Also we must have a registered domain name. We can use Route 53 as your domain registrar, or we can use a different registrar.

## In this topic
- [[CNAME vs Alias Records]]
- [[DNS Fundamentals]]
- [[Route 53 DNSSEC]]
- [[Route 53 Health Checks]]
- [[Route 53 Resolver]]
- [[Route 53 Routing Policies]]
- [[Route 53 TTL]]
- [[Third-Party Domains and Route 53]]

## Exam tasks
- [[Task 2.2 Design highly available and or or fault-tolerant architectures]]
- [[Task 4.4 Design cost-optimized network architectures]]

---
**Map:** [[Networking and Content Delivery Map]]
