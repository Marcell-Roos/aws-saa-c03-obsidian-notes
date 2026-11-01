---
tags: [service, cat/networking, scope/in]
---

# Third-Party Domains and Route 53

We buy or register our domain name with a Domain Registrar typically by paying annual charges. The Domain Registrar usually provides us with a [[DNS Fundamentals|DNS]] service to manage our DNS records, but we can use another DNS service to manage our DNS records.

If we buy a domain on a third party registrar, we can still use [[Amazon Route 53|Route 53]] as the DNS Service provider. First create a Hosted Zone in Route 53, then **update NS Records on third party website to use Route 53 Name Servers**.

---
**Up:** [[Amazon Route 53]] · **Map:** [[Networking and Content Delivery Map]]
