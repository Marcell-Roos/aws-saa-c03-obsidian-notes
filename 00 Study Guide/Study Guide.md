---
tags: [exam, scope/in]
aliases: ["Study Roadmap", "Study Plan"]
---

# Study Guide

This is your route from a first look at the exam to passing it. Work through it from top to bottom, ticking boxes as you go. Everything you need is in this vault.

> [!summary] The method in five lines
> 1. **Read** one chapter at a time, in order.
> 2. **Test yourself** at the end of each chapter, before moving on.
> 3. **Build it** in the [[Hands-On Labs]], because doing fixes knowledge.
> 4. **Log every mistake** in the [[Mistake Log]], and find out why you made it.
> 5. **Simulate the exam** with five timed practice exams, and take the real one only when you pass the readiness gate.

## Choose your pace

| Plan | Suits | Hours per week | Length |
| --- | --- | --- | --- |
| **Standard (recommended)** | Some IT experience, new to AWS | 10 to 12 | 10 weeks |
| **Fast** | Full-time study | 20 to 25 | 5 weeks |
| **Experienced** | Works with AWS already | 12 | 6 weeks. Skim chapters where you score 90% in the self-test first |
| **Relaxed** | Busy schedule | 6 to 7 | 16 weeks |

In total, expect about 115 hours. That is around 80 hours of chapters, 15 hours of labs and 20 hours of practice exams and review. The weekly split below is for the Standard plan. Other paces use the same steps in the same order.

> [!warning] No IT background?
> AWS suggests the Cloud Practitioner exam first for people with no IT experience. You can still follow this guide, but allow the Relaxed pace, and spend extra time on [[01 Cloud Foundations]] and [[09 VPC Fundamentals]].

## How to study a chapter

1. Read the info box at the top, to see why the chapter matters.
2. Read the chapter once at normal speed. Do not take notes yet.
3. Go back through it. For each table, cover the right-hand side, and try to say it aloud.
4. Redraw any diagrams from memory.
5. Do **Exam patterns**: cover the middle column, and answer from the left-hand column.
6. Do **Check yourself** with the answers folded. Open each answer only after you choose.
7. Score yourself. **Aim for 80% or more.** If you score lower, reread the sections you missed, and repeat the questions in a day or two.
8. Add every wrong answer to the [[Mistake Log]].

**Revise as you go.** At the start of each study session, spend ten minutes redoing the questions you got wrong last time. Spreading revision out works far better than cramming.

## The steps

### Step 0 Set up

**Standard plan: first day, about 2 hours.**

- [ ] Read [[SAA-C03 Exam Overview]]
- [ ] Read [[Exam Technique]]
- [ ] Skim the four domain pages: [[Domain 1 Design Secure Architectures|Domain 1]], [[Domain 2 Design Resilient Architectures|Domain 2]], [[Domain 3 Design High-Performing Architectures|Domain 3]], [[Domain 4 Design Cost-Optimized Architectures|Domain 4]]
- [ ] Do [[Hands-On Labs#Lab 0 Set up a safe AWS account|Lab 0]] to set up a safe AWS account with a budget alarm
- [ ] Pick a target exam date. Book it now if you can, because a date helps you keep going
- [ ] If English is not your first language, request ESL +30 before booking

### Step 1 Foundations and identity

**Standard plan: week 1. About 10 hours.** This is the base for everything else, and identity is the biggest single topic in the largest domain.

- [ ] Read [[01 Cloud Foundations]] and score at least 80% on its self-test
- [ ] Read [[02 IAM and Federation]] and score at least 80%
- [ ] Read [[03 Multi-Account Governance]] and score at least 80%
- [ ] Do [[Hands-On Labs#Lab 1 IAM roles and least privilege|Lab 1]]

**You can move on when you can:** explain policy evaluation without notes, say when to use a role instead of a resource policy, and say which of SCP, RCP and permission boundary fits a case.

### Step 2 Compute and scaling

**Standard plan: week 2. About 8 hours.**

- [ ] Read [[04 Amazon EC2]] and score at least 80%
- [ ] Read [[05 Load Balancing and Auto Scaling]] and score at least 80%
- [ ] Do [[Hands-On Labs#Lab 2 Load balancer and Auto Scaling|Lab 2]]

**You can move on when you can:** choose a purchasing option from a scenario, pick an instance family from a workload, and pick a load balancer and a scaling policy.

### Step 3 Storage

**Standard plan: week 3. About 11 hours.** S3 appears in every domain, so take your time.

- [ ] Read [[06 Amazon S3]] and score at least 80%
- [ ] Read [[07 S3 Security and Data Protection]] and score at least 80%
- [ ] Read [[08 Block and File Storage]] and score at least 80%
- [ ] Do [[Hands-On Labs#Lab 3 S3 versioning and lifecycle|Lab 3]]

**You can move on when you can:** choose a storage class from access frequency and retrieval time, choose an encryption type, and pick EBS, EFS, FSx or S3 for a workload.

### Step 4 Networking

**Standard plan: week 4. About 10 hours.** This is the hardest part for most people. Draw everything.

- [ ] Read [[09 VPC Fundamentals]] and score at least 80%
- [ ] Read [[10 VPC Connectivity and Hybrid Networking]] and score at least 80%
- [ ] Do [[Hands-On Labs#Lab 4 Build a VPC from scratch|Lab 4]]
- [ ] Draw a three-tier VPC across two AZs from memory, including the route tables

**You can move on when you can:** work out how many usable addresses a subnet has, explain why a request fails from flow log results, and choose between peering, Transit Gateway, PrivateLink, VPN and Direct Connect.

### Step 5 DNS and the edge

**Standard plan: week 5, first half. About 6 hours.**

- [ ] Read [[11 Route 53]] and score at least 80%
- [ ] Read [[12 CloudFront and Global Accelerator]] and score at least 80%
- [ ] Do [[Hands-On Labs#Lab 5 Private S3 site behind CloudFront|Lab 5]]

**You can move on when you can:** choose a routing policy from a requirement, and say when to use CloudFront, Global Accelerator or Transfer Acceleration.

### Step 6 Databases

**Standard plan: weeks 5 and 6. About 9 hours.**

- [ ] Read [[13 RDS and Aurora]] and score at least 80%
- [ ] Read [[14 DynamoDB]] and score at least 80%
- [ ] Read [[15 ElastiCache and Other Databases]] and score at least 80%
- [ ] Do [[Hands-On Labs#Lab 6 DynamoDB and a read replica|Lab 6]]

**You can move on when you can:** explain Multi-AZ versus read replicas, calculate RCU and WCU, and pick a database from a data model.

### Step 7 Serverless and containers

**Standard plan: weeks 6 and 7. About 9 hours.**

- [ ] Read [[16 Lambda and Serverless]] and score at least 80%
- [ ] Read [[17 API Gateway and Front-End Services]] and score at least 80%
- [ ] Read [[18 Containers]] and score at least 80%
- [ ] Read [[19 Other Compute Services]] and score at least 80%
- [ ] Do [[Hands-On Labs#Lab 7 Serverless API|Lab 7]]

**You can move on when you can:** say when Lambda is the wrong answer, tell a task role from an execution role, and choose a Beanstalk deployment policy.

### Step 8 Integration and data

**Standard plan: weeks 7 and 8. About 9 hours.**

- [ ] Read [[20 Messaging and Integration]] and score at least 80%
- [ ] Read [[21 Streaming and Data Ingestion]] and score at least 80%
- [ ] Read [[22 Data Lakes and Analytics]] and score at least 80%
- [ ] Do [[Hands-On Labs#Lab 8 Fan-out with SNS and SQS|Lab 8]]

**You can move on when you can:** choose between SQS, SNS, EventBridge and Kinesis, explain Firehose versus Data Streams, and choose between Athena, Redshift and EMR.

### Step 9 Security and operations

**Standard plan: week 8. About 9 hours.**

- [ ] Read [[23 Encryption and Secrets]] and score at least 80%
- [ ] Read [[24 Threat Protection and Security Services]] and score at least 80%
- [ ] Read [[25 Monitoring and Auditing]] and score at least 80%
- [ ] Read [[26 Infrastructure as Code and Operations]] and score at least 80%
- [ ] Do [[Hands-On Labs#Lab 9 Encryption and audit|Lab 9]]

**You can move on when you can:** match every security service to its job, say which of CloudWatch, CloudTrail or Config answers a question, and explain key policies.

### Step 10 Migration, recovery, cost and design

**Standard plan: week 9. About 11 hours.**

- [ ] Read [[27 Migration and Data Transfer]] and score at least 80%
- [ ] Read [[28 High Availability and Disaster Recovery]] and score at least 80%
- [ ] Read [[29 Cost Optimisation]] and score at least 80%
- [ ] Read [[30 Machine Learning Services]] and score at least 80%
- [ ] Read [[31 Architecture Patterns]] and score at least 80%
- [ ] Do [[Hands-On Labs#Lab 10 Infrastructure as code and a budget|Lab 10]]
- [ ] Go through all four domain pages. For each row, explain the middle column without looking. Follow the link for anything you cannot explain

**You can move on when you can:** choose a DR strategy from an RPO, RTO and budget, and walk through the case studies with the solutions covered.

### Step 11 Practice exams

**Standard plan: week 10, and more if needed. About 20 hours.**

Treat each attempt like the real thing: 130 minutes, one sitting, phone away, no notes. Record your answers on paper or in a separate note, so that you are not tempted to open the answers.

- [ ] Sit [[Practice Exam 1]]
- [ ] Review **every** question, including the ones you got right, and add mistakes to the [[Mistake Log]]
- [ ] Reread the sections behind your weakest domain
- [ ] Sit [[Practice Exam 2]], at least two days later
- [ ] Review it in the same way
- [ ] Sit [[Practice Exam 3]]
- [ ] Review it in the same way
- [ ] Sit [[Practice Exam 4]]
- [ ] Review it in the same way
- [ ] Sit [[Practice Exam 5]] last. It is the hardest, with longer scenarios in which two options often work
- [ ] Review it in the same way

A full review takes about as long as the exam itself. It is where most of the learning happens, so do not skip it.

### Step 12 The readiness gate

**Book or keep your exam only if all of these are true:**

- [ ] You scored **80% or more** on [[Practice Exam 3]] and [[Practice Exam 4]], on a first attempt
- [ ] You scored **75% or more** on [[Practice Exam 5]], on a first attempt
- [ ] No domain is under 70% in those attempts
- [ ] You can explain the middle column of all four domain pages
- [ ] You can answer the [[Final Review Cheat Sheet]] traps table with the right-hand side covered
- [ ] Your [[Mistake Log]] has no repeating topic that you have not fixed

The exam's passing score of 720 is a scaled score, and AWS does not publish how it maps to a percentage. These targets include a safety margin, but they are estimates and not a promise, because these exams have not been calibrated against the real one. If you want one more check, try AWS's free Official Practice Question Set.

If you do not pass the gate, go to [[#If you are not ready yet]].

### Step 13 The final days

- [ ] Three days before: read the [[Final Review Cheat Sheet]] in full
- [ ] Two days before: redo everything in your [[Mistake Log]]
- [ ] One day before: light review only, and check your ID, route or system test
- [ ] On the day: follow the checklist at the end of [[Exam Technique]]

## If you are not ready yet

| Result | What to do |
| --- | --- |
| Under 60% | You have knowledge gaps. Go back to the weakest domain's main chapters, and redo their self-tests before any more mocks |
| 60% to 70% | Find your weakest two domains. Spend a week on them, then retake one exam |
| 70% to 80% | You are close. Work through the [[Mistake Log]], read [[Exam Technique]] again, and retake |
| Over 80%, but only on repeats | You may be remembering answers. Explain why each wrong option is wrong, without looking |

Retakes of the same practice exam are useful for review, but they overstate your readiness, so use first-attempt scores for the gate.

## If you fail the real exam

It happens to many people. Your score report may show how you did in each section, so use it to pick your weakest domains. You can retake the exam after 14 calendar days, for the full fee.

## Tracking your progress

| Step | Date started | Date finished | Self-test average |
| --- | --- | --- | --- |
| 1. Foundations and identity | | | |
| 2. Compute and scaling | | | |
| 3. Storage | | | |
| 4. Networking | | | |
| 5. DNS and the edge | | | |
| 6. Databases | | | |
| 7. Serverless and containers | | | |
| 8. Integration and data | | | |
| 9. Security and operations | | | |
| 10. Migration, recovery, cost and design | | | |

| Practice exam | Date | Score | Domain 1 | Domain 2 | Domain 3 | Domain 4 |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | | | | | | |
| 2 | | | | | | |
| 3 | | | | | | |
| 4 | | | | | | |
| 5 | | | | | | |

---
**Home:** [[Home]]
