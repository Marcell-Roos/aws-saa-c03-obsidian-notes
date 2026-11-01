---
tags: [comparison, scope/in]
---

# SCPs vs RCPs vs Permission Boundaries

| | [[Service Control Policies]] | [[Resource Control Policies]] | [[IAM Permission Boundaries]] |
| --- | --- | --- | --- |
| Limits | Principals in member accounts | Resources in member accounts | One user or role |
| Attached to | Root, OU, account | Root, OU, account | User or role |
| Grants access | Never | Never | Never |
| Management account | Not affected | Not affected | Applies |

---
**Up:** [[Comparisons Map]]
