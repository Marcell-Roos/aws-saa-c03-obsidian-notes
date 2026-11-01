---
tags: [service, cat/storage, scope/in]
aliases: ["Storage Lens"]
---

# S3 Storage Lens

With **Storage Lens** we can analyze and optimize storage across entire AWS Organization or AWS Accounts. We can discover anomalies, identify cost efficiencies and apply data protection best practices across entire AWS Organization.

It is possible to aggregate data for Organization, specific accounts, regions, buckets or prefixes.

Can be configured to export metrics daily to an [[Amazon S3|S3 bucket]] (CSV, [[Data Formats|Parquet]]).

**Default Dashboard** - visualizes summarized insights and trends for both free and advanced metrics. It shows Multi-Region and Multi-Account data. It is preconfigured by S3 and cannot be deleted but can be disabled.

**Storage Lens Metrics**

- **Summary Metrics** - general insights about our S3 storage (StorageBytes, ObjectCount…). It is used for identifying the fastest-grownig (or not used) buckets and prefixes.
- **Cost-Optimization Metrics** - provide insights to manage and optimize our storage costs (NonCurrentVersionStorageBytes, IncompleteMultiPartUploadStorageBytes…). It is used for **identifying buckets with incomplete multipart** uploaded older than 7 days and which objects could be transitioned to lower cost storage class.
- **Data-Protection Metrics** - provide insights for data protection features. It is used for identifying buckets that aren't following data-protection best practices.
- **Access-Management Metrics** - provide insights for S3 object ownership. It is used for identifying which object ownership settings our buckets use.
- **Event Metrics** - provide insights for [[S3 Event Notifications]].
- **Performance Metrics** - provide insights for [[S3 Performance|S3 Transfer Acceleration]].
- **Activity Metrics** - provide insights about how our storage is requested.
- **Detailed Status Code Metrics** - provide insights for HTTP status codes.

**Free Metrics** - automatically available for all customers. Data is available for queries for 14 days.

**Advanced Metrics and Recommendations** - paid metrics and features (advanced metrics, [[Amazon CloudWatch|CloudWatch]] publishing, prefix aggregation). Data is available for queries for 15 months.

---
**Up:** [[Amazon S3]] · **Map:** [[Storage Map]]
