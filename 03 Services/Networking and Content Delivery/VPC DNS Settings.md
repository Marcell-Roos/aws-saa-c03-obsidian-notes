---
tags: [service, cat/networking, scope/in]
---

# VPC DNS Settings

When we launch an [[Amazon EC2|EC2 instance]] into a **default [[Amazon VPC|VPC]]**, AWS provides it with public and private [[DNS Fundamentals|DNS]] hostnames that correspond to the public IPv4 and private IPv4 addresses for the instance.

When we launch an instance into a **non-default VPC**, AWS provides the instance with a private DNS hostname only. New instances will only be provided with a public DNS hostname depending on these two DNS attributes: the **DNS resolution** and **DNS hostnames** that we have specified for our VPC and if our instance has a public IPv4 address.

---
**Up:** [[Amazon VPC]] · **Map:** [[Networking and Content Delivery Map]]
