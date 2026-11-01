---
tags: [service, cat/analytics, scope/in]
aliases: ["OpenSearch", "Amazon OpenSearch"]
---

# Amazon OpenSearch Service

With **OpenSearch** we can search any field, even partially matches. It’s common to use OpenSearch as a complement to another database. It does not natively support SQL (can be enabled via a plugin). It comes with OpenSearch Dashboards for visualization.

There are two modes: managed cluster and serverless cluster.

- **Solution Architecture - OpenSearch [[Amazon DynamoDB|DynamoDB]] Integration.** [[DynamoDB Streams]] trigger [[AWS Lambda|Lambda]], which indexes items in OpenSearch for search, while DynamoDB stays the source of truth.

- **Solution Architecture - OpenSearch [[CloudWatch Logs]] Integration.** A subscription filter sends logs to Lambda or [[Amazon Data Firehose|Firehose]], which load them into OpenSearch.

- **Solution Architecture - OpenSearch [[Kinesis Data Streams|KDS]] and Firehose Integration.** Data Firehose loads a stream directly into OpenSearch, while Kinesis Data Streams needs a Lambda consumer or Firehose.

---
**Map:** [[Analytics Map]]
