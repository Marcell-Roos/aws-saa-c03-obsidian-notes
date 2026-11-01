---
tags: [exam, scope/in]
---

# Exam Technique

- **Read the last sentence first.** The actual question and its qualifier usually live there.
- **Find the qualifier.** It decides between two working answers.
- **Eliminate two.** Most questions have two clearly wrong options.
- **Budget about 2 minutes per question** (130 minutes for 65 questions). Flag anything that passes 90 seconds and move on.
- **Answer everything.** There's no penalty for guessing.

| Qualifier in the question | Prefer |
| --- | --- |
| Most cost-effective | The cheapest option that still meets every requirement |
| Least operational overhead | Managed or serverless |
| Highly available | Multi-AZ |
| Survive a Region failure | Multi-Region |
| Most secure | Least privilege, private connectivity, encryption, temporary credentials |
| Without changing the application | Infrastructure-level services such as [[RDS Proxy]] or a [[Elastic Load Balancing\|load balancer]] |
| Real time | [[Kinesis Data Streams]] rather than Data [[Amazon Data Firehose\|Firehose]] |
| Decouple | [[Amazon SQS\|SQS]], [[Amazon SNS\|SNS]] or [[Amazon EventBridge\|EventBridge]] |

---
**Up:** [[SAA-C03 Exam Overview]]
