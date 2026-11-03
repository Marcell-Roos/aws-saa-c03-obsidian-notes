---
tags: [topic, cat/compute, scope/in]
aliases: ["AWS Lambda", "Lambda", "Lambda Concurrency", "Lambda in a VPC", "Lambda Invocation Models", "Lambda SnapStart", "Lambda Environment Variable Encryption", "AWS Serverless Application Repository", "Serverless Patterns", "Drill Lambda"]
---

# Lambda and Serverless

> [!info] Why this matters
> "Serverless" is the exam's favourite answer to "least operational overhead". You need to know when Lambda fits, when it does not, and how it connects to other services.
>
> **Covers:** serverless in [[Domain 2 Design Resilient Architectures#Task 2.1|Task 2.1]], [[Domain 3 Design High-Performing Architectures#Task 3.2|Task 3.2]], [[Domain 4 Design Cost-Optimized Architectures#Task 4.2|Task 4.2]].
> **Study time:** about 3 hours.

## What serverless means

Serverless means no servers to provision or patch, automatic scaling, and paying only for what you use. The servers still exist, but AWS runs them. Common building blocks are Lambda, Fargate, API Gateway, DynamoDB, S3, SQS, SNS, EventBridge and Step Functions.

## AWS Lambda

**AWS Lambda** runs your code in response to events, with no servers to manage.

- Functions are **stateless**. Keep state in DynamoDB, S3 or ElastiCache.
- It scales automatically, by running more copies in parallel.
- It integrates with most AWS services, and with many programming languages.
- Logs and metrics go to CloudWatch. Tracing goes to X-Ray.

**Pricing:** you pay per request and for compute time, in GB-seconds. The free tier includes 1 million requests and 400,000 GB-seconds per month. Graviton (arm64) functions offer better price-performance.

### Limits

Memorise this table. Many questions turn on these numbers.

| Setting | Limit |
| --- | --- |
| Memory | 128 MB to 10,240 MB. **CPU scales with memory** |
| Timeout | **15 minutes** |
| `/tmp` storage | 512 MB to 10,240 MB |
| Deployment package | 50 MB zipped, 250 MB unzipped, 10 GB container image |
| Payload | 6 MB synchronous, 1 MB asynchronous, 200 MB streamed response |
| Environment variables | 4 KB |
| Layers | 5 |
| Concurrency | 1,000 per Region by default. New accounts start lower |
| Scaling rate | 1,000 execution environments every 10 seconds, per function |

Two reasoning points follow from this table:

- A job longer than 15 minutes cannot run in standard Lambda. (Lambda Managed Instances functions can run up to 90 minutes when invoked asynchronously or through most event source mappings, but expect 15 minutes as the exam answer.) Use Fargate, ECS or AWS Batch. If it can be split into shorter steps, use [[20 Messaging and Integration#AWS Step Functions|Step Functions]].
- A CPU-bound function that is too slow needs **more memory**, because there is no separate CPU setting.

### Packaging

- A **layer** is a ZIP with libraries or a custom runtime, shared between functions.
- A **container image** up to 10 GB can run on Lambda, if it implements the Lambda Runtime API. Only Linux containers are supported.
- A **function URL** gives a function its own HTTPS endpoint, with `AWS_IAM` or no authentication.
- A function can mount an **EFS** file system, for shared persistent storage across invocations. It must be attached to the VPC.

### How functions are invoked

| Model | Examples | What happens on failure |
| --- | --- | --- |
| **Synchronous** | API Gateway, ALB, function URLs | The caller gets the error and must handle it |
| **Asynchronous** | S3 events, SNS, EventBridge | Lambda retries twice, then sends to a dead-letter queue or a destination |
| **Event source mapping** (polling) | SQS, Kinesis Data Streams, DynamoDB Streams, MSK | Lambda polls in batches. Failures return to the queue, or block a shard until handled |

For asynchronous invocations, configure a **dead-letter queue** (SQS or SNS) or, better, an **on-failure destination**, so that events are not lost after the retries.

For SQS, messages that keep failing should go to a dead-letter queue on the **source queue**.

### Event source mappings in detail

With a polling source, Lambda reads batches for you, so the behaviour on failure depends on the source.

| Source | How it reads | On failure | Settings to know |
| --- | --- | --- | --- |
| **SQS** | Batches, scaling up with the backlog | The batch returns to the queue after the visibility timeout. A DLQ on the queue catches repeat failures | Set the queue's visibility timeout to at least **six times** the function timeout. Report partial batch failures, so that only failed messages are retried |
| **Kinesis, DynamoDB Streams** | One batch at a time per shard, in order | The batch retries until it succeeds or expires, and **blocks the shard** | Set a maximum retry count, split failing batches, and add an on-failure destination |

If an SQS queue's visibility timeout is shorter than the function's run time, the message reappears while it is still being processed, and the work happens twice.

The metric `IteratorAge` shows how far a stream consumer has fallen behind. A rising value means that you should add shards, raise the parallelisation factor, or speed up the function.

### Cold starts and concurrency

A **cold start** is the delay when Lambda creates a new execution environment and runs your initialisation code.

| Feature | What it does | Cost |
| --- | --- | --- |
| **Reserved concurrency** | Sets aside capacity for a function, and **caps** it at that level | Free |
| **Provisioned concurrency** | Keeps environments initialised, which **removes cold starts** | Extra charge |
| **SnapStart** | Restores from a snapshot of the initialised function, for up to 10 times faster start-up | Free for Java. Charged for Python and .NET |

Each execution environment handles **one request at a time**. So the concurrency you need is simple arithmetic:

> [!example] Working out concurrency
> Concurrency = requests per second × average duration in seconds.
> 100 requests per second at 500 ms needs 50 concurrent environments.
> 800 requests per second at 1.5 seconds needs 1,200, which is above the default quota of 1,000, so this function would be throttled unless you request an increase.
> Making the function faster lowers the concurrency that it needs.

The exam distinction: **Reserved caps and guarantees. Provisioned keeps warm.**

Reserved concurrency also protects a fragile downstream system, because it limits how many copies can run. Because Lambda can scale very quickly, set a CloudWatch alarm on `ConcurrentExecutions` or `Invocations`.

### Versions and aliases

A **version** is an immutable copy of a function, and an **alias** is a named pointer to one, such as `prod`. An alias can split traffic between two versions, which gives you canary releases, and it lets you roll back by moving the pointer.

### Lambda in a VPC

By default, Lambda runs outside your VPC and cannot reach private resources such as RDS or ElastiCache. To reach them, configure the VPC ID, subnets and security groups. Lambda then creates network interfaces in your subnets, and its role needs permission for this.

- A VPC-attached function **loses internet access** unless traffic goes through a NAT gateway. Putting it in a public subnet does not help, because it does not get a public IP.
- To reach AWS services privately, use VPC endpoints.
- When connecting to RDS, use [[13 RDS and Aurora#RDS Proxy|RDS Proxy]] to avoid exhausting connections. The function must be in the VPC, because the proxy is never public.

### Execution environment

An environment is reused for later requests, which has practical effects:

- Code **outside the handler** runs only once per environment. Put SDK clients and database connections there.
- `/tmp` and global variables can survive between invocations in the same environment. They can be used as a cache, but must not be relied on.
- Each environment is separate, so state in one is not visible to another.

### Security

- Permissions come from the **execution role**.
- A **resource-based policy** controls what can invoke the function, such as S3 or another account.
- Environment variables are encrypted at rest by default, but they are still visible to anyone who can view the function. Use encryption helpers for sensitive values, or better, keep secrets in Secrets Manager or Parameter Store.

### Monitoring

| Metric | Tells you |
| --- | --- |
| `Invocations` | How often the function ran |
| `Errors` | Failures in your code |
| `Throttles` | Requests rejected because of concurrency limits |
| `Duration` | How long each run took. It drives cost |
| `ConcurrentExecutions` | How many environments are in use |
| `IteratorAge` | Lag on stream sources |

### Scheduled jobs

An EventBridge schedule that invokes Lambda is a **serverless cron job**, which replaces an EC2 instance kept running only to run a script.

### Newer options

AWS documents several newer Lambda features that are not in the exam guide, so you only need to recognise them:

- **Durable functions** coordinate long-running work with checkpoints, for up to a year overall. Each invocation is still limited to 15 minutes.
- **Lambda Managed Instances** run functions on EC2 instances in your account.
- **Web Functions** run web applications as serverless HTTP servers.

## AWS Serverless Application Repository

A catalogue for finding, sharing and deploying serverless applications built with the AWS Serverless Application Model (SAM).

- Teams can deploy a pre-built application without cloning, building, packaging or publishing its source code first.
- Applications can be shared privately, with specific AWS accounts, or publicly.
- There is no additional charge for the repository. You pay only for the resources the deployed application uses.

## When to use serverless

| Use Lambda when | Use something else when |
| --- | --- |
| Work is short and event-driven | A job runs longer than 15 minutes |
| Traffic is spiky or unpredictable | Traffic is steady and heavy, where EC2 or containers can be cheaper |
| You want no servers to manage | The app needs a long-lived process or a heavy runtime |
| You are gluing services together | You need OS-level access or GPUs |

See [[19 Other Compute Services#Choosing compute|Choosing compute]] and [[31 Architecture Patterns#Serverless web application|the serverless web application pattern]].

## Exam patterns

| If the question says | Think | Why |
| --- | --- | --- |
| 90-minute job | Not Lambda. Use Batch or Fargate | 15-minute limit |
| Job can be divided into short steps | Step Functions | |
| Generate a thumbnail on upload | S3 event to Lambda | |
| Latency spikes after idle periods | Provisioned concurrency | Removes cold starts |
| Java function has slow start-up, avoid extra cost | SnapStart | Free for Java |
| Lambda overwhelms a legacy database | Reserved concurrency, RDS Proxy | Cap and pool |
| Lambda must reach a private RDS database | Attach to the VPC, and use RDS Proxy | |
| VPC Lambda lost internet access | NAT gateway or VPC endpoints | No public IP |
| CPU-intensive function too slow | Increase memory | CPU scales with it |
| Run a script nightly with no servers | EventBridge schedule to Lambda | |
| Async function fails and events disappear | DLQ or on-failure destination | |
| Process SQS messages | Event source mapping | Lambda polls in batches |
| Dependencies over 250 MB | Container image | Up to 10 GB |
| Share code across functions | Layers | |
| Function needs permissions | Execution role | |
| Short-lived HTTP endpoint with no API Gateway | Function URL | |

## Check yourself

**1.** A video transcoding task takes around 90 minutes. The company wants a serverless approach. What should it use?

- A. Lambda with maximum memory
- B. AWS Batch or a Fargate task
- C. Lambda with reserved concurrency
- D. API Gateway

> [!success]- Answer
> **B.** Lambda stops at 15 minutes. Batch on Fargate handles long-running jobs with no servers to manage.

**2.** An API behind API Gateway and Lambda is fast most of the time, but it has latency spikes after quiet periods. What is the most direct fix?

- A. Reserved concurrency
- B. Provisioned concurrency
- C. Increase the timeout
- D. Add a dead-letter queue

> [!success]- Answer
> **B.** Provisioned concurrency keeps environments initialised, so that requests avoid cold starts. Reserved concurrency only guarantees capacity.

**3.** A Lambda function that processes images is slow, and CloudWatch shows it is CPU-bound. How can the team give it more CPU?

- A. Set a CPU value on the function
- B. Increase the memory
- C. Increase the timeout
- D. Add a layer

> [!success]- Answer
> **B.** Lambda allocates CPU in proportion to memory.

**4.** A Lambda function must connect to an RDS database in a private subnet. Under load it causes connection errors. Which steps solve this? (Choose two.)

- A. Attach the function to the VPC
- B. Use RDS Proxy
- C. Move the database to a public subnet
- D. Add a layer with the database driver
- E. Increase `/tmp` storage

> [!success]- Answer
> **A and B.** The function needs VPC access, and the proxy pools connections.

**5.** After attaching a Lambda function to a private subnet, calls to an external API time out. What should be added?

- A. A NAT gateway in a public subnet, with a route from the private subnet
- B. A public IP on the function
- C. An internet gateway route from the private subnet
- D. More memory

> [!success]- Answer
> **A.** VPC-attached functions have no public IP, so they need NAT for internet access.

**6.** A function is invoked asynchronously by S3. Some events fail repeatedly and vanish. What should the team configure?

- A. Provisioned concurrency
- B. An on-failure destination or a dead-letter queue
- C. A longer TTL
- D. A function URL

> [!success]- Answer
> **B.** After two retries, failed events are dropped unless a destination or DLQ captures them.

**7.** A company has a small legacy database that can handle only 50 connections. A Lambda function that uses it occasionally overwhelms it. What is the simplest way to limit this?

- A. Set reserved concurrency to a low value
- B. Increase the memory
- C. Use provisioned concurrency
- D. Use SnapStart

> [!success]- Answer
> **A.** Reserved concurrency caps how many copies can run at once.

**8.** A nightly housekeeping script runs on a dedicated EC2 instance that sits idle the rest of the day. How can the company reduce cost and overhead?

- A. Use a larger instance
- B. Use an EventBridge schedule to invoke a Lambda function
- C. Use a Savings Plan
- D. Use Spot Instances with no schedule

> [!success]- Answer
> **B.** This removes the idle server entirely, as long as the script runs in under 15 minutes.

---
**Previous:** [[15 ElastiCache and Other Databases]] · **Next:** [[17 API Gateway and Front-End Services]] · **Plan:** [[Study Guide]]
