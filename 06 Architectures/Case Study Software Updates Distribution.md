---
tags: [architecture, scope/in]
---

# Case Study Software Updates Distribution

We have an application running on [[Amazon EC2|EC2]] that distributes software updates once in a while. When a new software update is out, we get a lot of requests and the content is distributed in mass over the network and it’s very costly.

We can use [[Amazon CloudFront|CloudFront]]. It will cache software update files at the edge and no changes are needed to the architecture. Software update files are not dynamic, they are static (never changing).

EC2 instances aren't serverless, but CloudFront is and it will scale for us. We will save in availability, network bandwidth cost, etc.

---
**Up:** [[Architecture Patterns]]
