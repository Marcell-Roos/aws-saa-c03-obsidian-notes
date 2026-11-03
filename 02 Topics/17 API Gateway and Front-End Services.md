---
tags: [topic, cat/frontend, scope/in]
aliases: ["Amazon API Gateway", "API Gateway", "API Gateway Advanced Features", "API Gateway Authorizers and Integrations", "AWS Amplify", "Amplify", "AWS AppSync", "AppSync", "AWS Device Farm", "Drill API Gateway"]
---

# API Gateway and Front-End Services

> [!info] Why this matters
> API creation and management is named in [[Domain 2 Design Resilient Architectures#Task 2.1|Task 2.1]], and throttling in [[Domain 4 Design Cost-Optimized Architectures#Task 4.4|Task 4.4]]. API Gateway is the front door of most serverless designs.
>
> **Study time:** about 1.5 hours.

## Amazon API Gateway

**API Gateway** is a fully managed service to create, publish, secure and monitor APIs. It is serverless and scales automatically. You pay for API calls and data transferred out.

### API types

| Type | Best for | Notes |
| --- | --- | --- |
| **REST API** | Full feature set | API keys, usage plans, caching, request validation, WAF |
| **HTTP API** | Simple, low-cost proxies | Much cheaper and faster. JWT authorisers, fewer features |
| **WebSocket API** | Two-way real-time messaging | Chat, live dashboards |

### REST or HTTP API

| Feature | REST API | HTTP API |
| --- | --- | --- |
| Cost | Higher | Much lower |
| Usage plans and API keys | Yes | No |
| Response caching | Yes | No |
| AWS WAF | Yes | No |
| Request validation | Yes | No |
| Private endpoints | Yes | No |
| Edge-optimised endpoints | Yes | No, Regional only |
| Lambda authorisers | Yes | Yes |
| JWT authorisers | Through Cognito | Built in |
| IAM authorisation | Yes | Yes |

Choose an HTTP API unless you need something in the REST column. The exam often offers it as the cheaper way to front Lambda.

### Endpoint types

| Endpoint | For | Notes |
| --- | --- | --- |
| **Edge-optimised** | Global clients | Routed through CloudFront edge locations. The API still lives in one Region |
| **Regional** | Clients in the same Region | Can be combined with your own CloudFront distribution for more control |
| **Private** | Only within a VPC | Reached through an interface VPC endpoint. Use a resource policy |

### Integrations

| Integration | What it does |
| --- | --- |
| **Lambda** | Invokes a function. **Lambda proxy** passes the whole request through |
| **HTTP** | Calls an HTTP backend, on AWS or elsewhere. **HTTP proxy** passes it through |
| **AWS service** | Calls a service directly, such as putting records on Kinesis, or starting a Step Functions state machine |
| **Mock** | Returns a fixed response without a backend |

**Mapping templates** can transform requests and responses when not using proxy mode.

A direct AWS service integration can remove a Lambda function that only forwards data. Between API Gateway and a private backend, a **VPC link** reaches an NLB or ALB in your VPC.

### Direct service integrations

API Gateway can call other AWS services without any Lambda function in between. This removes code, cost and latency.

| Pattern | Benefit |
| --- | --- |
| API Gateway to **SQS** | Accepts requests quickly and buffers them |
| API Gateway to **Kinesis** | Ingests records from clients |
| API Gateway to **DynamoDB** | Simple reads and writes |
| API Gateway to **Step Functions** | Starts a workflow and returns at once |
| API Gateway to **S3** | Simple object access. For large files, return a presigned URL, because payloads are limited to 10 MB |

### Security

| Option | Use |
| --- | --- |
| **IAM** | Internal AWS callers, with SigV4-signed requests |
| **Cognito user pool authoriser** | App users with JWT tokens |
| **Lambda authoriser** | Custom logic, or third-party tokens |
| **Resource policy** | Limit by account, IP range or VPC endpoint |
| **AWS WAF** | Web exploits and rate limits, on REST APIs |
| **API keys** | Identifying clients for usage plans. **Not** an authentication method |

For a **custom domain**, use a certificate from ACM. An edge-optimised endpoint needs the certificate in **us-east-1**, and a Regional endpoint needs it in the API's Region. Then add a Route 53 Alias record.

### Throttling and usage plans

API Gateway protects your backend by throttling.

- The default is **10,000 requests per second** per account, per Region.
- Limits can be set at account, stage, method or usage plan level.
- Clients over the limit receive **HTTP 429**.

A **usage plan** sets who can call an API, how fast and how much, using API keys. This is how a SaaS company offers pricing tiers, such as a free tier at 100 requests per day.

Throttling is also a cost control, because it stops runaway clients driving up backend charges.

### Caching

REST APIs can cache responses per stage. The default TTL is **300 seconds**. This reduces calls to the backend and improves latency, at an hourly cost.

### Limits

| Limit | Value |
| --- | --- |
| Integration timeout | **29 seconds** by default. It can be raised for Regional and private APIs |
| Payload | 10 MB |
| Account throttle | 10,000 requests per second by default |

If a backend takes minutes, do not wait for it. **Go asynchronous:** return `202 Accepted`, put the work on SQS or start a Step Functions workflow, and let the client check later. This is the right design even where the timeout could be raised. Older material treats 29 seconds as a hard limit.

### WebSocket APIs

A WebSocket API keeps a two-way connection open. The routes `$connect`, `$disconnect` and `$default` invoke your back end. Applications usually store each connection ID in DynamoDB, and send messages to clients through a callback URL. Use this for chat, live dashboards and notifications.

### CORS

Browser JavaScript on another domain needs **CORS enabled** on the API, or the browser blocks the response.

### Monitoring and deployment

- CloudWatch provides usage, latency and error metrics, and access logs.
- X-Ray can trace requests.
- **Stages** such as `dev` and `prod` are separate deployments of an API.
- **Canary deployments** on a stage send a percentage of traffic to a new version.

## AWS AppSync

**AppSync** is a managed **GraphQL** service, with real-time subscriptions. Clients ask for exactly the data they want from one endpoint, and AppSync gathers it from sources such as DynamoDB, Lambda and RDS.

- **Resolvers** decide how queries fetch data.
- It supports Cognito, API keys, IAM and OIDC for authentication.
- Authorisation can go down to individual fields.

It is not on the in-scope list, but "GraphQL" in a question points to it.

## AWS Amplify

**Amplify** is a set of tools for building and hosting full-stack web and mobile applications. It handles hosting with CI/CD from a Git repository, and it connects front-ends to back-end services such as authentication and data.

If a question describes a front-end team wanting to build and host a web or mobile app quickly, think Amplify.

Amplify Hosting deploys to the AWS global content delivery network (CDN). It supports SSR frameworks such as Next.js, single-page apps such as React and Angular, and static site generators. Feature branches give separate environments, and pull request previews show changes during code review.

## AWS Device Farm

**Device Farm** tests web and mobile apps on real devices hosted by AWS. "Test on many real phones" points here.

You can run automated tests on many devices in parallel by uploading your app and tests, or open a device in your browser for manual testing. Test hosts and devices can connect to your VPC to reach private endpoints.

## Exam patterns

| If the question says | Think | Why |
| --- | --- | --- |
| REST API with no servers, pay per request | API Gateway, Lambda, DynamoDB | The standard chain |
| Different request limits for each pricing tier | Usage plans and API keys | REST API |
| Mobile users must sign in before calling the API | Cognito user pool authoriser | |
| Existing third-party token system | Lambda authoriser | Custom logic |
| Cheapest simple HTTP proxy to Lambda, JWT auth | HTTP API | |
| Live dashboard or chat | WebSocket API | |
| API only reachable within a VPC | Private endpoint | Interface endpoint |
| Global clients | Edge-optimised endpoint | |
| Backend takes 2 minutes and requests time out | Go asynchronous with SQS or Step Functions | Return 202 |
| Browser blocked calling the API | Enable CORS | |
| Clients receive 429 errors | Throttling | Raise the limit or add caching |
| Reduce backend load for repeated requests | API Gateway caching | 300-second default |
| Protect an API from SQL injection | WAF | On a REST API |
| GraphQL | AppSync | |
| Host a web app from Git | Amplify | |
| Test on real phones | Device Farm | |

## Check yourself

**1.** A SaaS company wants to give free-tier customers 1,000 requests per day and paid customers 100,000 requests per day. What should it use?

- A. API Gateway usage plans and API keys
- B. WAF rules
- C. Lambda reserved concurrency
- D. Cognito groups

> [!success]- Answer
> **A.** Usage plans define quotas and throttle rates for each set of API keys.

**2.** A company has its own token-based authentication, and it wants API Gateway to validate those tokens. Which option fits?

- A. IAM authorisation
- B. Cognito user pools
- C. A Lambda authoriser
- D. API keys

> [!success]- Answer
> **C.** A Lambda authoriser runs custom logic to validate third-party tokens.

**3.** A backend report takes three minutes to generate, and clients calling it through API Gateway receive timeouts. What is the best design?

- A. Increase Lambda memory
- B. Return 202, queue the work with SQS or Step Functions, and let the client fetch the result later
- C. Use a WebSocket API for every request
- D. Add API Gateway caching

> [!success]- Answer
> **B.** Long-running work should be asynchronous, so that no client holds a connection open for minutes.

**4.** An internal API must be reachable only from within a company's VPC. What should the architect use?

- A. An edge-optimised endpoint with an API key
- B. A private endpoint with an interface VPC endpoint and resource policy
- C. A Regional endpoint with a public IP
- D. CloudFront signed URLs

> [!success]- Answer
> **B.** Private APIs are reached only through an interface endpoint.

**5.** Many clients make the same GET requests, and the backend database is under pressure. Which API Gateway feature helps most?

- A. Stage caching
- B. Mapping templates
- C. Lambda authorisers
- D. Canary deployments

> [!success]- Answer
> **A.** Responses are served from the cache without calling the backend.

**6.** A team needs a very low-cost API that simply proxies requests to a Lambda function and validates JWTs. Which API type should it choose?

- A. REST API
- B. HTTP API
- C. WebSocket API
- D. Private REST API

> [!success]- Answer
> **B.** HTTP APIs are cheaper and simpler, and they support JWT authorisers.

**7.** API keys alone are being used to secure an API that handles sensitive data. Why is this not sufficient?

- A. API keys are only for WebSocket APIs
- B. API keys identify clients for usage plans, but they are not an authentication mechanism
- C. API keys expire after an hour
- D. API keys cannot be rotated

> [!success]- Answer
> **B.** Use IAM, Cognito or a Lambda authoriser for authentication.

---
**Previous:** [[16 Lambda and Serverless]] · **Next:** [[18 Containers]] · **Plan:** [[Study Guide]]
