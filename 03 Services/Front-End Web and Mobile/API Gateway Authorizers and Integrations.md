---
tags: [service, cat/front-end, scope/in]
aliases: ["Authorizers", "Lambda Proxy"]
---

# API Gateway Authorizers and Integrations

**Authorizers**

| Option | Use |
| --- | --- |
| [[AWS IAM\|IAM]] | Internal AWS callers, signed with SigV4 |
| [[Amazon Cognito\|Cognito]] user pools | App users with JWT tokens |
| [[AWS Lambda\|Lambda]] authorizer | Custom logic or third-party tokens |

**Integrations:** Lambda proxy passes the whole request to the function. HTTP proxy passes it to a backend URL. Mapping templates can transform requests when not using proxy mode.

**Caching:** responses can be cached per stage, with a default TTL of 300 seconds. **Throttling:** set at account, stage, method or usage plan level, and clients receive a 429 error when they exceed it.

---
**Up:** [[Amazon API Gateway]] · **Map:** [[Front-End Web and Mobile Map]]
