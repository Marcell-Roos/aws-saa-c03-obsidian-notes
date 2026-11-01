---
tags: [service, cat/management, scope/in]
aliases: ["CloudWatch Alarm", "Composite Alarms"]
---

# CloudWatch Alarms

**CloudWatch Alarms** - used to trigger notifications for any metrics. It has various options (sampling, percentage, max, min, etc). With CloudWatch Alarm we can stop, terminate, reboot or recover an [[Amazon EC2|EC2 instance]], trigger auto scaling action or send notification to [[Amazon SNS|SNS]].

Alarm States: OK, INSUFFICIENT_DATA, ALARM.

Period - length of time in seconds to evaluate the metrics.

**Composite Alarms** - monitoring the states of multiple other alarms and we can use AND and OR conditions to merge them.

There is a status check to check the EC2 and we can define a CloudWatch Alarm to monitor a specific EC2 instance. In case the alarm is being breached, we can start an EC2 instance recovery or send an alert to our SNS topic.

Alarms can be created based on [[CloudWatch Logs]] Metrics Filters.

---
**Up:** [[Amazon CloudWatch]] · **Map:** [[Management and Governance Map]]
