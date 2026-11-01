---
tags: [service, cat/security, scope/in]
---

# IAM Policies for S3

**[[AWS IAM|IAM]] for [[Amazon S3|S3]]**

**s3:ListBucket** - applies to arn:aws:s3:::test (**bucket level permission**).

**s3:GetObject**, **s3:PutObject**, **s3:DeleteObject** - applies to arn:aws:s3:::test/* (**object level permission**).

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowAuroraToExampleBucket",
            "Effect": "Allow",
            "Action": [
                "s3:PutObject",
                "s3:GetObject",
                "s3:AbortMultipartUpload",
                "s3:ListBucket",
                "s3:DeleteObject",
                "s3:GetObjectVersion",
                "s3:ListMultipartUploadParts"
            ],
            "Resource": [
                "arn:aws:s3:::amzn-s3-demo-bucket/*",
                "arn:aws:s3:::amzn-s3-demo-bucket"
            ]
        }
    ]
}
```

---
**Up:** [[AWS IAM]] · **Map:** [[Security Identity and Compliance Map]]
