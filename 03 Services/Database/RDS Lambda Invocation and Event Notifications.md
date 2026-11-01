---
tags: [service, cat/database, scope/in]
---

# RDS Lambda Invocation and Event Notifications

We can invoke [[AWS Lambda|Lambda functions]] from within our DB instance. It allows us to process data events from within a database. It’s **supported for [[Amazon RDS|RDS]] for Postgres and [[Amazon Aurora|Aurora]] MySQL**.

We must allow outbound traffic to our Lambda function from within our DB instance (Public, [[NAT Gateways|NAT Gateway]], [[VPC Endpoints]]). DB instance must have the required permissions to invoke the Lambda.

**Event Notifications** - notifications that tell information about the DB instance itself. It is near real-time event. We don't have any information about the data itself. Can send notifications to [[Amazon SNS|SNS]] or subscribe to events using [[Amazon EventBridge|EventBridge]].

Need to subscribe to the following event categories: DB instance, DB snapshot, DB Parameter Group, DB [[Security Groups|Security Group]], [[RDS Proxy]], Custom Engine Version.

---
**Up:** [[Amazon RDS]] · **Map:** [[Database Map]]
