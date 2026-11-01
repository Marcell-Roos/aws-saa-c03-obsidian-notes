---
tags: [comparison, scope/in]
---

# Standard vs Express Workflows

| | Standard | Express |
| --- | --- | --- |
| Max duration | 1 year | 5 minutes |
| Semantics | Exactly-once | At-least-once (async), at-most-once (sync) |
| Use | Long, auditable, non-idempotent | High-volume, idempotent |

See [[AWS Step Functions]].

---
**Up:** [[Comparisons Map]]
