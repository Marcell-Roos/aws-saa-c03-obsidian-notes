---
tags: [service, cat/networking, scope/in]
aliases: ["SNI", "Server Name Indication"]
---

# ELB SSL Certificates and SNI

**SSL Certificate** allows traffic between our clients and our [[Elastic Load Balancing|load balancer]] to be encrypted in transit. They have an expiration date and must be renewed. Public SSL certificates are issued by CA (Certificate Authorities).

- SSL (Secure Sockets Layer) - used to encrypt connections.
- TLS (Transport Layer Security) - successor to SSL.

We can manage certificates using [[AWS Certificate Manager|ACM]] and can create and upload our own certificates alternatively. The load balancer uses an X.509 certificate (SSL/TLS server certificate).

**HTTPS Listener** - a configuration that enables the load balancer to handle HTTPS. We must specify a default certificate and can add an optional list of certificates to support multiple domains. Clients can use **SNI (Server Name Indication)** to specify the hostname they reach. Also we have ability to specify a security policy to support older versions of SSL/TLS (legacy clients).

**Server Name Indication (SNI)** - solves the problem of loading multiple SSL certificates onto one web server (to serve multiple websites). It is a newer protocol and requires the client to indicate the hostname of the target server in the initial SSL handshake. It only works with **[[Application Load Balancer|ALB]], [[Network Load Balancer|NLB]] & [[Amazon CloudFront|CloudFront]]**.

ALB & NLB support multiple listeners with multiple SSL certificates and use SNI to make it work.

---
**Up:** [[Elastic Load Balancing]] · **Map:** [[Networking and Content Delivery Map]]
