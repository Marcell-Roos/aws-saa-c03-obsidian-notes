---
tags: [service, cat/security, scope/in]
aliases: ["ACM"]
---

# AWS Certificate Manager

**ACM** lets us easily provision, manage and deploy TLS certificates. Used to provide HTTPS for websites. It supports both public and private TLS certificates.

Can be integrated with (load TLS certificates on) [[Elastic Load Balancing|ELB]], [[Amazon CloudFront|CloudFront]] distributions, APIs on [[Amazon API Gateway|API Gateway]].

**ACM Private CA** - for enterprise customers building a public key infrastructure (PKI) inside the AWS cloud and is intended for private use within an organization. We can create our own CA hierarchy and issue certificates with it for authenticating internal users, computers, applications, services… Certificates issued by a private CA are trusted only within our organization, not on the internet.

**Importing Public Certificates**

There is an option to generate the certificate outside of ACM and then import it. Because there is **no automatic renewal**, we must import a new certificate before expiry. ACM sends daily expiration events, starting 45 days prior to expiration (number of days can be configured). Those events are appearing in [[Amazon EventBridge|EventBridge]].

[[AWS Config]] has a managed rule named *acm*-*certificate-expiration-check* to check for expired certificates.

**Integration with [[Application Load Balancer|ALB]]**

Attach an ACM certificate to an HTTPS listener, and redirect HTTP to HTTPS with a listener rule. TLS terminates at the load balancer.

**Integration with API Gateway**

First, we need to create a custom domain name in API Gateway. ACM can be integrated with Edge-Optimized and Regional endpoints in API Gateway.

- Edge-Optimized Endpoint (default) - the TLS certificate must be in us-east-1 (CloudFront's certificate Region).
- Regional Endpoint - TLS Certificate must be imported on API Gateway in the same region as the API Stage.

Then we need to setup CNAME or [[CNAME vs Alias Records|Alias record]] in [[Amazon Route 53|Route 53]].

The **[[AWS IAM|IAM]] certificate store** holds server certificates in IAM for Regions where ACM isn't available. Prefer ACM where possible: IAM can't issue or auto-renew certificates.

ACM certificates for CloudFront must be in **us-east-1**. ACM-issued public certificates renew automatically. Imported ones don't.

## Exam tasks
- [[Task 1.3 Determine appropriate data security controls]]

---
**Map:** [[Security Identity and Compliance Map]]
