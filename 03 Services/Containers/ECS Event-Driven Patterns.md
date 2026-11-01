---
tags: [service, cat/containers, scope/in]
---

# ECS Event-Driven Patterns

- **Tasks Invoked by [[Amazon EventBridge|Event Bridge]].**
    - Amazon EventBridge listens to events from AWS services, custom applications, or SaaS integrations.
    - A rule is created in EventBridge that matches certain event patterns.
    - When an event matching the rule occurs, EventBridge triggers [[Amazon ECS|ECS]] task or other service to process that event.
    - For example, if an [[Amazon S3|S3]] object is created, an EventBridge rule can trigger a specific ECS [[AWS Fargate|Fargate]] task to process the file.

- **Tasks Invoked by Event Bridge Schedule.**
    - EventBridge can be configured to run on a cron or rate expression (e.g. every hour).
    - A scheduled rule in EventBridge invokes ECS tasks on the defined schedule.
    - For example, we can run a scheduled ECS task every day at midnight to perform batch processing.

- **ECS - [[Amazon SQS|SQS]] Queue.**
    - Messages are sent to an SQS queue by producers, which can be other services, APIs, or applications.
    - An ECS service with a task or set of tasks polls the SQS queue for messages.
    - When a message is retrieved, the ECS task processes it. Once processed, the message is either deleted or moved to a dead-letter queue if it fails.

- **Intercept Stopped Tasks using Event Bridge.**
    - ECS emits task state change events (e.g. task stopped, task started) which are sent to EventBridge.
    - An EventBridge rule is set up to capture the “ECS Task State Change” events where the stopped status is detected.
    - When a task stops, EventBridge triggers a target such as an [[Amazon SNS|SNS]] topic, [[AWS Lambda|Lambda function]], or another ECS task for handling remediation, alerting, or cleanup actions.

---
**Up:** [[Amazon ECS]] · **Map:** [[Containers Map]]
