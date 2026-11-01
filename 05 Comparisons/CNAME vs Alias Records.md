---
tags: [comparison, scope/in]
aliases: ["Alias record", "Alias records", "CNAME record"]
---

# CNAME vs Alias Records

AWS Resources expose an AWS hostname and if we want we can map that hostname to a domain we own.

**CNAME** - maps an alias domain name to a true or canonical domain name. Essentially, it redirects one domain name to another (app.mydomain.com ⇒ test.anything.com). Can be used only for non root domain.

**Alias** - specific to AWS [[Amazon Route 53|Route 53]] and provide a more powerful and flexible option compared to CNAME records. They can map domain names to AWS resources (app.mydomain.com ⇒ test.amazonaws.com). It works with root domain (apex domain) and non root domain. It is free of charge.

Alias record is always of type A/AAAA for AWS resources. It automatically recognizes changes in the resource’s IP addresses. We cannot set the TTL when we have Alias record because Route 53 does it for us.

**Alias Record Targets**

[[Elastic Load Balancing|ELB]] load balancers, [[Amazon CloudFront|CloudFront]] distributions, [[Amazon API Gateway|API Gateway]], [[AWS Elastic Beanstalk|Elastic Beanstalk]] environments, [[Amazon S3|S3]] website endpoints, [[Amazon VPC|VPC]] interface endpoints, [[AWS Global Accelerator|Global Accelerator]], and records in the same hosted zone. An Alias **can't** point to an [[Amazon EC2|EC2]] [[DNS Fundamentals|DNS]] name.

---
**Up:** [[Amazon Route 53]]
