---
tags: [service, cat/storage, scope/in]
aliases: ["Glacier Select"]
---

# S3 Select

> [!warning] Closed to new customers
> S3 Select and Glacier Select have been in maintenance since 25 July 2024. Use Athena or client-side filtering for new designs.

**S3 Select & Glacier Select** retrieves less data using SQL by performing server-side filtering. It can filter by rows and columns. We have less network transfer and less CPU cost on client-side. We can perform S3 Select to query only the necessary data inside the CSV files based on the bucket's name and the object's key.

---
**Up:** [[Amazon S3]] · **Map:** [[Storage Map]]
