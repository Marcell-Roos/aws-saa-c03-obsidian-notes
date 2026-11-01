---
tags: [service, cat/application, scope/in]
aliases: ["visibility timeout"]
---

# SQS Visibility Timeout

After a message is polled by a consumer, it becomes invisible to other consumers. By default, the message visibility timeout is 30s (max 12h). After the message visibility timeout is over, the message is visible in [[Amazon SQS|SQS]].

If a message is not processed within the visibility timeout, it will be processed twice. A consumer could call the ChangeMessageVisibility API to get more time.

If visibility timeout is high (hours), and consumer crashes, re-processing will take time and if visibility timeout is too low (seconds), we may get duplicates.

---
**Up:** [[Amazon SQS]] · **Map:** [[Application Integration Map]]
