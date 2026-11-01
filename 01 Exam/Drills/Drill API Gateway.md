---
tags: [drill, scope/in]
---

# Drill API Gateway

Adapted from [RonitSachdev/aws-saa-c03-guides](https://github.com/RonitSachdev/aws-saa-c03-guides) (CC BY 4.0), with outdated facts changed.

## Question patterns

- *"Build a REST API with no servers to manage, pay only per request"* → **[[Amazon API Gateway|API Gateway]] + [[AWS Lambda|Lambda]] + [[Amazon DynamoDB|DynamoDB]]** (the canonical serverless chain)
- *"SaaS company wants to offer customers different API request limits per pricing tier"* → **Usage Plans + API Keys** (REST API only — per-customer tiers)
- *"Mobile app users must sign in before calling the API"* → **[[Amazon Cognito|Cognito User Pool]] authorizer** (app users = Cognito JWTs)
- *"Company has an existing custom/third-party token system for API auth"* → **Lambda Authorizer** (custom logic = your Lambda decides)
- *"Cheapest way to expose a simple Lambda function over HTTP with JWT auth"* → **HTTP API** (~70% cheaper, minimal features)
- *"Push live updates to a real-time dashboard / chat application"* → **WebSocket API** (persistent two-way connection)
- *"API must be accessible only from within the [[Amazon VPC|VPC]], never the internet"* → **Private endpoint + Interface [[VPC Endpoints|VPC Endpoint]]**
- *"Backend process takes 2 minutes; API Gateway requests keep timing out — fix it"* → **Go async: return 202, queue to [[Amazon SQS|SQS]]/Step Functions** (29s is a hard limit; you cannot raise it)
- *"Browser JavaScript from another domain gets blocked calling the API"* → **Enable [[S3 CORS|CORS]]** on API Gateway
- *"Clients suddenly receive HTTP 429 errors"* → **Throttling** — raise the limit or add caching/usage plans

## Pocket card

| Keyword | Answer |
|---|---|
| Serverless REST API | API GW + Lambda + DynamoDB |
| API keys / usage plans / caching / [[AWS WAF\|WAF]] | REST API (only) |
| Lowest cost, simple proxy, JWT | HTTP API |
| Real-time / chat / live push | WebSocket API |
| Global clients | Edge-Optimized endpoint |
| VPC-only API | Private endpoint (Interface Endpoint) |
| AWS-service callers | [[AWS IAM\|IAM]] / SigV4 auth |
| App users sign in | Cognito User Pool authorizer |
| Custom/third-party tokens | Lambda Authorizer |
| 429 errors | Throttling (default 10,000 req/s) |
| Backend > 29 seconds | Async: 202 + SQS/Step Functions |
| Cache TTL default | 300 seconds |
| Browser cross-domain error | Enable CORS |

---
**Up:** [[Drills Map]]
