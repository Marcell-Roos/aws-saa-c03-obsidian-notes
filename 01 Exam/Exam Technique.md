---
tags: [exam, scope/in]
---

# Exam Technique

Knowing AWS is not quite the same as passing this exam. Questions usually have two answers that would work, and your task is to find the one that fits the words in the question. This page shows how.

## How a question is built

A typical question has four parts:

1. **A situation.** A company, its current setup and a change it wants to make.
2. **Requirements.** Numbers, constraints and facts that rule things out.
3. **A qualifier.** "Most cost-effective", "least operational overhead" and so on.
4. **Options.** Usually one wrong, one that sounds right but is not, and two that could work.

## A method for every question

1. **Read the last sentence first.** This tells you what is being asked and gives you the qualifier.
2. **Read the scenario, and pick out the hard requirements.** Look for numbers, "must", "without", "existing", and names of technologies.
3. **Predict the answer** before reading the options, if you can.
4. **Remove anything that breaks a requirement.** Most questions have two options you can rule out quickly.
5. **Use the qualifier to choose** between what is left.
6. **Answer, flag if unsure, and move on.** Do not leave any question blank.

## The qualifier decides

| Qualifier in the question | Prefer |
| --- | --- |
| **Most cost-effective** | The cheapest option that still meets every requirement |
| **Least operational overhead** | Managed or serverless, with the fewest moving parts |
| **Highly available** | Multi-AZ |
| **Survive a Region failure** | Multi-Region |
| **Fault tolerant** | Works through a failure with no interruption |
| **Most secure** | Least privilege, private connectivity, encryption, temporary credentials |
| **Without changing the application** | Infrastructure-level services such as RDS Proxy or a load balancer |
| **Lowest latency** | In-memory cache, edge services, the same AZ |
| **Real time** | Kinesis Data Streams rather than Data Firehose |
| **Decouple** | SQS, SNS or EventBridge |
| **Long-term** or **steady** | Reserved or Savings Plans |
| **Temporary** or **short-lived** | STS, On-Demand, or instance store for data |
| **Existing** (software, skills or tools) | The service that keeps them, such as Amazon MQ or EKS |
| **Near real time** | Firehose |

Words that seem small can change the answer:

| Wording | Effect |
| --- | --- |
| "Automatically" | Rules out anything manual, such as read replica promotion |
| "With the least effort" | Prefer a built-in feature over a custom script |
| "Prevent" | SCP, IAM or Object Lock. Config only detects |
| "Detect" or "monitor" | Config, GuardDuty or CloudWatch |
| "All accounts" | Organizations, Control Tower, Firewall Manager, StackSets |
| "Globally" | CloudFront, Global Accelerator, or global tables |
| "Without internet" | VPC endpoints, Direct Connect or PrivateLink |
| "Cannot be interrupted" | Rules out Spot |
| "Can tolerate interruption" | Points to Spot |

## Multiple-response questions

The question says how many to choose, such as "Choose two". AWS does not publish exactly how these are marked, so assume that you need every selection right to earn the mark.

- Treat each option as true or false.
- The correct options often work together, or cover two separate requirements.
- When two options contradict each other, at most one is correct.

## Spotting wrong answers

Wrong answers are usually wrong for a predictable reason.

| A wrong answer often... | Example |
| --- | --- |
| Solves a different problem | Multi-AZ to improve read performance |
| Uses a service that cannot do it | CloudFront for UDP |
| Works, but costs far more than needed | Multi-Region for an AZ failure |
| Adds needless custom work | A Lambda script for something a feature does |
| Keeps long-lived credentials | Access keys on an instance |
| Uses a legacy or retired service | Classic Load Balancer |
| Is out of scope | Amazon Lightsail, AWS CodeDeploy |
| Exceeds a limit | Lambda for a one-hour job |
| Is more operational work | Installing a database on EC2 when RDS would do |

General preferences that hold in most questions:

- Managed beats self-managed.
- Roles beat access keys.
- Private beats public.
- Automatic beats manual.
- Built-in features beat custom code.
- The simplest solution that meets the requirements wins.

## Time plan

You have 130 minutes for 65 questions, which is 2 minutes each.

| Pass | Time | What to do |
| --- | --- | --- |
| First pass | About 90 minutes | Answer everything. Flag anything over 90 seconds and move on |
| Second pass | About 30 minutes | Return to flagged questions |
| Final check | About 10 minutes | Make sure nothing is blank |

Long questions take more time, and short ones can be done in 30 seconds, so do not check the clock on each one. Check every 13 questions: you should have used about 26 minutes.

When you return to a flagged question, change your answer only if you find a reason. Do not change it because of a vague feeling.

## When you do not know

1. Rule out what you can.
2. Prefer the option with managed services, least privilege and fewer moving parts.
3. Pick one. A blank answer scores nothing, and there is no penalty for guessing.

Fifteen questions do not count, so one strange question may be an unscored one. Do not let it shake you.

## Older exam wording

AWS updates services faster than exam questions. A question may reflect how a service worked a little while ago, so if the current fact and the question's assumption differ, answer the question as written. This vault notes where old and new differ, such as gp3 limits or the old FIPS rule for CloudHSM.

## The day before

Do not cram new material. Read [[Final Review Cheat Sheet]], get some sleep, and check your route or your system test.

## On the day

- [ ] Bring the right ID, or have it ready online.
- [ ] Eat beforehand, and drink water.
- [ ] Arrive 30 minutes early, or start check-in 30 minutes before.
- [ ] Use the flag feature, and remember the Help button for service names.
- [ ] Trust your preparation.

---
**Previous:** [[SAA-C03 Exam Overview]] · **Next:** [[Final Review Cheat Sheet]] · **Plan:** [[Study Guide]]
