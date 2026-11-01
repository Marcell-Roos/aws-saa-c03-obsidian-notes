---
tags: [service, cat/application, scope/unlisted]
aliases: ["SWF"]
---

# Amazon SWF

> [!note] Exam scope
> Not on AWS's in-scope or out-of-scope list. The in-scope list is non-exhaustive, so treat this as background.

**SWF (Simple Workflow Service)** is a fully managed service that helps us coordinate and manage complex workflows. It allows us to build and run applications that coordinate tasks across distributed components or microservices.

- **Workflow** - series of steps or tasks that need to be executed in a specific order or with specific dependencies. SWF helps us manage the execution of these workflows, ensuring that tasks are completed and handling retries and failures.
- **Activity** - task that is performed as part of the workflow. Activities are typically implemented as code that performs the work and communicates with external systems or services.
- **Task** - unit of work within an activity or a workflow. Tasks are sent to worker processes that perform the actual work.

---
**Up:** [[AWS Step Functions]] · **Map:** [[Application Integration Map]]
