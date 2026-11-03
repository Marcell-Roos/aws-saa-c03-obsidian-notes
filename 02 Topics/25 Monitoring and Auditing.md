---
tags: [topic, cat/management, scope/in]
aliases: ["Amazon CloudWatch", "CloudWatch", "CloudWatch Agent", "CloudWatch Alarms", "CloudWatch Insights", "CloudWatch Logs", "CloudWatch Metric Filters", "CloudWatch Metrics", "AWS CloudTrail", "CloudTrail", "AWS Config", "Config Conformance Packs", "CloudWatch vs CloudTrail vs Config", "AWS X-Ray", "X-Ray", "AWS Health Dashboard", "Amazon Managed Grafana", "Amazon Managed Service for Prometheus", "AWS Trusted Advisor", "Trusted Advisor", "Drill CloudWatch CloudTrail Config"]
---

# Monitoring and Auditing

> [!info] Why this matters
> Almost every architecture needs monitoring, and the exam tests which tool answers which question. "Workload visibility" and "metrics to deliver high availability" are in [[Domain 2 Design Resilient Architectures#Task 2.2|Task 2.2]], and audit trails support [[Domain 1 Design Secure Architectures|Domain 1]].
>
> **Study time:** about 2.5 hours.

## Which tool answers which question?

| Service | Question it answers |
| --- | --- |
| **Amazon CloudWatch** | How is it **performing**? |
| **AWS CloudTrail** | **Who** did what, and when? |
| **AWS Config** | **What** did it look like, and is it compliant? |
| **AWS X-Ray** | Where is the request slow? |
| **AWS Trusted Advisor** | Are we following best practices? |
| **AWS Health Dashboard** | Is AWS itself having a problem that affects us? |

## Amazon CloudWatch

CloudWatch collects metrics and logs, raises alarms and shows dashboards.

### Metrics

A **metric** is a variable to monitor, such as `CPUUtilization`. It belongs to a namespace, and it has **dimensions**, such as instance ID.

- EC2 reports metrics every **5 minutes** by default, or every minute with **detailed monitoring**.
- **Memory and disk space inside the instance are not default metrics.** Hypervisor-level metrics such as CPU, network and disk I/O are.
- **Custom metrics** can be published through the API or the agent.
- **Metric Streams** send metrics in near real time to Data Firehose or to third parties such as Datadog.

### CloudWatch agent

The **unified CloudWatch agent** runs on EC2 or on-premises servers. It collects logs and system-level metrics such as RAM, processes and disk space. Configuration can be stored in Parameter Store. It needs IAM permissions. The older CloudWatch Logs agent sends only logs.

### Logs

**CloudWatch Logs** stores log data, encrypted by default.

- **Log groups** usually represent an application.
- **Log streams** are instances or containers within it.
- Retention can be from one day to forever. Set it to control cost.

Logs come from Elastic Beanstalk, ECS, Lambda, CloudTrail, Route 53, the agent and more.

| Feature | Purpose |
| --- | --- |
| **Metric filter** | Turns a log pattern into a metric, such as counting `ERROR` lines, so an alarm can act on it |
| **Logs Insights** | Interactive queries with a purpose-built language. Not real time |
| **Export to S3** | Batch export, which can take up to 12 hours. Use it for archiving |
| **Subscription filter** | **Real-time** stream to Kinesis Data Streams, Firehose, Lambda or OpenSearch |

To gather logs across accounts and Regions, send subscription filters in each account to a destination in a central account, usually through Kinesis and Firehose into S3.

### Alarms

**Alarms** watch a metric and act when it crosses a threshold.

| State | Meaning |
| --- | --- |
| `OK` | Within the threshold |
| `ALARM` | Past the threshold |
| `INSUFFICIENT_DATA` | Not enough data |

Actions include notifying SNS, scaling an ASG, and stopping, terminating, rebooting or **recovering** an EC2 instance. **Composite alarms** combine several alarms with AND and OR, to reduce noise.

### Events

**Amazon EventBridge** was formerly called CloudWatch Events, and older questions may use that name. Use it to react to state changes, such as an instance stopping or a CloudTrail API call.

**CloudWatch Synthetics** runs scripted checks that act like users, so that you learn about a failure before customers do. **Cross-account observability** lets one monitoring account view metrics and logs from many accounts.

### Insights features

| Feature | Monitors |
| --- | --- |
| **Container Insights** | ECS, EKS and Kubernetes metrics and logs |
| **Lambda Insights** | System-level metrics for functions, such as cold starts |
| **Contributor Insights** | Top talkers, such as the heaviest network users or the URLs with the most errors |
| **Application Insights** | Automated dashboards for potential application problems |
| **Database Insights** | Query and workload performance for RDS and Aurora |

### Choosing metrics

"Identifying metrics based on business requirements" means choosing a signal that reflects the user's experience.

| Workload | Useful metric |
| --- | --- |
| Web tier | `RequestCountPerTarget`, target response time, 5xx errors |
| Worker tier | Queue depth, backlog per instance |
| Database | `DatabaseConnections`, `FreeStorageSpace`, read and write latency |
| Lambda | `Errors`, `Throttles`, `Duration`, `ConcurrentExecutions` |
| NAT gateway or network | Bytes, connection errors |

## AWS CloudTrail

**CloudTrail** records API calls in your account: who did what, from where and when. Calls from the console, CLI and SDKs, and calls made by services, are all recorded.

- **Event history** is on by default and keeps **90 days** of management events.
- For longer retention, create a **trail**, which delivers to **S3**, and optionally to CloudWatch Logs.
- Trails can cover all Regions, or one.
- An **organisation trail** covers every account.
- **Log file integrity validation** proves that logs were not changed.

| Event type | Examples | Default |
| --- | --- | --- |
| **Management events** | Creating a bucket, changing a security group | Logged |
| **Data events** | S3 object reads, Lambda invocations | **Not logged**, because of the volume. Opt in, at extra cost |
| **Insights events** | Unusual API activity, such as a spike | Optional |

To react to an API call, use EventBridge. For example: alert when someone creates an IAM user.

To query logs, use Athena on S3. CloudTrail Lake closed to new customers on 31 May 2026.

## AWS Config

**AWS Config** records the configuration of your resources over time, and it checks them against rules.

Questions it answers:

- Is there unrestricted SSH access in my security groups?
- Do my buckets have public access?
- How has my ALB configuration changed?

Facts to remember:

- It is a **per-Region** service, and can be aggregated across Regions and accounts.
- It is charged per item recorded and per rule evaluation.
- Rules are AWS managed, or custom, using Lambda or Guard.
- **Rules detect, and they do not prevent.** To prevent an action, use an SCP or an IAM policy.
- Non-compliance can notify through SNS or EventBridge.

**Automatic remediation** uses Systems Manager Automation documents, with retries if a resource stays non-compliant.

**Conformance packs** bundle Config rules and remediations, and deploy them as one unit across accounts and Regions.

## AWS X-Ray

**X-Ray** traces requests through distributed applications. It shows a service map, and pinpoints latency and errors. Choose it when a question asks which microservice is slow. CloudWatch gives metrics and logs, and X-Ray gives per-request traces. It works with Lambda, API Gateway, ECS, EC2 and others.

X-Ray does not trace every request. By default, the X-Ray SDK records the first request each second, and five percent of any additional requests. Sampling rules can change this.

## AWS Health Dashboard

| View | Shows |
| --- | --- |
| **Service health** | The general status of AWS services across Regions, with history and an RSS feed |
| **Your account** | Events that affect your own resources, with remediation guidance |

**AWS Health** events can go to EventBridge, for automated responses. For example, you can act when AWS plans maintenance on your instance.

## AWS Trusted Advisor

**Trusted Advisor** analyses your account and gives recommendations in six categories: cost optimisation, performance, security, fault tolerance, service limits and operational excellence.

- The basic plan gets service limit checks, and selected security and fault tolerance checks.
- The full set of checks, and programmatic access through the AWS Support API, need Business Support+ or a higher plan.

It is not on AWS's in-scope list by name, but it appears in many questions, for instance on idle instances, open security groups and approaching quotas.

| Tool | Focus |
| --- | --- |
| Trusted Advisor | Broad best-practice checks |
| AWS Config | Your own resource compliance rules |
| Compute Optimizer | Rightsizing with machine learning. See [[29 Cost Optimisation#AWS Compute Optimizer\|Cost Optimisation]] |
| Well-Architected Tool | A guided workload review |

## Grafana and Prometheus

**Amazon Managed Grafana** provides managed Grafana dashboards for metrics, logs and traces from many sources, including on-premises. It integrates with IAM Identity Center.

**Amazon Managed Service for Prometheus** is managed Prometheus-compatible monitoring for containers, usually viewed in Grafana. Pick these two when a scenario already uses open-source Grafana or Prometheus.

## Exam patterns

| If the question says | Think | Why |
| --- | --- | --- |
| Who terminated an instance last week? | CloudTrail | |
| Alert when EC2 memory exceeds 80% | CloudWatch agent, custom metric, alarm | Not a default metric |
| Alarm on more than 100 `ERROR` lines | Metric filter and alarm | |
| Security group's configuration last Tuesday | AWS Config | Timeline |
| Automatically fix non-compliant resources | Config rule and SSM Automation | |
| Prevent anyone disabling CloudTrail | SCP | Config only detects |
| Which microservice is slow? | X-Ray | |
| Process log entries in real time | Subscription filter | |
| Query logs interactively | Logs Insights | |
| Who downloaded an S3 object? | CloudTrail data events | Opt-in |
| Keep audit logs for 7 years, tamper-evident | Trail to S3, log file validation, Object Lock | |
| Alert when an IAM user is created | EventBridge rule on the CloudTrail event | |
| Unusual spike in API calls | CloudTrail Insights | |
| Too many separate alarms | Composite alarm | |
| Recover an instance on failed status checks | CloudWatch alarm recover action | |
| Top talkers | Contributor Insights | |
| Warned before reaching a service quota | Trusted Advisor | Or Service Quotas alarms |
| Identify idle instances and unattached Elastic IPs | Trusted Advisor | |
| Is AWS having an outage affecting me? | AWS Health Dashboard | |

## Check yourself

**1.** A production instance was terminated last week, and the team needs to find out who did it. Which service answers this?

- A. Amazon CloudWatch
- B. AWS CloudTrail
- C. AWS Config
- D. AWS X-Ray

> [!success]- Answer
> **B.** CloudTrail records API calls, including the identity of the caller.

**2.** The team wants an alarm when memory use on EC2 instances goes over 80%. What must it do?

- A. Enable detailed monitoring
- B. Install the CloudWatch agent to publish a memory metric, then create an alarm
- C. Create an AWS Config rule
- D. Use CloudTrail Insights

> [!success]- Answer
> **B.** Memory is not a default metric, because the hypervisor cannot see inside the OS.

**3.** A compliance team wants to know if any security group allows SSH from the internet, and to fix it automatically. What should be used?

- A. CloudTrail
- B. AWS Config with a rule and SSM Automation remediation
- C. CloudWatch Logs
- D. AWS X-Ray

> [!success]- Answer
> **B.** Config evaluates the resources, and Automation fixes them.

**4.** A team needs to process log events within seconds of being written, and send them to a Lambda function. What should it use?

- A. Export to S3
- B. Logs Insights
- C. A subscription filter
- D. A metric filter

> [!success]- Answer
> **C.** Subscription filters stream logs in real time. Export can take up to 12 hours.

**5.** A request crosses ten microservices, and users report slowness. Which tool shows where the time goes?

- A. CloudTrail
- B. X-Ray
- C. AWS Config
- D. Trusted Advisor

> [!success]- Answer
> **B.** X-Ray traces each request across services.

**6.** Auditors need proof that API logs have not been changed, and they must be kept for seven years. What is the best approach? (Choose two.)

- A. Create a trail with log file integrity validation
- B. Deliver the trail to S3 with suitable lifecycle and Object Lock settings
- C. Rely on the default 90-day event history
- D. Use CloudWatch metrics
- E. Use X-Ray

> [!success]- Answer
> **A and B.** Validation proves integrity, and S3 provides long-term, protected storage.

**7.** A team needs to see which S3 objects a specific role read. CloudTrail is on with default settings, but the reads do not appear. Why?

- A. CloudTrail does not support S3
- B. Data events are not logged by default
- C. The role was deleted
- D. The bucket must be public

> [!success]- Answer
> **B.** Object-level events must be enabled, and they cost extra.

**8.** The company wants to stop accounts from turning off AWS Config. What should it use?

- A. A Config rule
- B. An SCP
- C. A CloudWatch alarm
- D. Trusted Advisor

> [!success]- Answer
> **B.** Config rules only detect. SCPs prevent.

**9.** An operations team wants to alert only when CPU is high and network traffic is also high, to reduce false alarms. What should it use?

- A. Composite alarm
- B. Metric Streams
- C. Logs Insights
- D. A CloudTrail trail

> [!success]- Answer
> **A.** Composite alarms combine alarms with AND and OR.

---
**Previous:** [[24 Threat Protection and Security Services]] · **Next:** [[26 Infrastructure as Code and Operations]] · **Plan:** [[Study Guide]]
