---
tags: [service, cat/application, scope/in]
aliases: ["Long Polling", "long polling"]
---

# SQS Long Polling

**Long Polling** - when a consumer requests messages from the queue, it can optionally wait for messages to arrive if there are none in the queue.

Long Polling decreases the number of API calls made to [[Amazon SQS|SQS]] while increasing the efficiency and latency of our application. The **wait time can be between 1-20 seconds**.

It can be enabled at the queue level or at the API level using **WaitTimeSeconds**.

---
**Up:** [[Amazon SQS]] · **Map:** [[Application Integration Map]]
