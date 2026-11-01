---
tags: [service, cat/security, scope/in]
---

# aws PrincipalOrgID

**aws:PrincipalOrgID** - can be used in any resource policies to restrict access to accounts that are member of an AWS Organization.

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": [
          "s3:PutObject",
          "s3:GetObject"
      ],
      "Resource": "arn:aws:s3:::2022-financial-data/*",
      "Condition": {
        "StringEquals": {
          "aws:PrincipalOrgID": "o-sabhong3hu"
        }
      }
    }
  ]
}
```

---
**Up:** [[AWS Organizations]] · **Map:** [[Security Identity and Compliance Map]]
