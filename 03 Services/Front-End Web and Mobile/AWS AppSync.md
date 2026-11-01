---
tags: [service, cat/front-end, scope/unlisted]
aliases: ["AppSync"]
---

# AWS AppSync

> [!note] Exam scope
> Not on AWS's in-scope or out-of-scope list. The in-scope list is non-exhaustive, so treat this as background.

**AWS AppSync** is a fully managed service that simplifies the development of GraphQL and real-time APIs by enabling us to build scalable applications with ease. It **acts as a bridge** between our clients (such as web or mobile apps) and our data sources (like [[Amazon DynamoDB|DynamoDB]], [[AWS Lambda|Lambda]], [[Amazon RDS|RDS]], and other AWS services). It manages the complex backend work such as authentication, **caching**, data synchronization, and access control.

AppSync provides real-time updates to connected clients, making it ideal for use cases requiring instant data synchronization.

- **AppSync Resolvers** - determine how GraphQL queries or mutations should fetch or manipulate data.
- **AppSync Mapping Templates** - transform incoming requests into the appropriate format for the backend and then return the response.

**AppSync Security**

AppSync integrates with multiple AWS authentication providers, such as **[[Amazon Cognito]]**, API keys, [[AWS IAM|IAM]], or OpenID Connect (OIDC). We can implement fine-grained access control using role-based permissions and authorization rules.

**Field-level Authorization** - we can restrict access down to specific fields in our GraphQL schema, ensuring only authorized users can access sensitive data.

- **Solution Architecture - Access to Multiple [[Microservices]].** A single GraphQL endpoint fronts several backends, so clients make one request and AppSync gathers the data.

---
**Map:** [[Front-End Web and Mobile Map]]
