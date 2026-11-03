---
tags: [exam, scope/in]
aliases: ["Labs"]
---

# Hands-On Labs

AWS recommends a year of hands-on experience for this exam. These labs give you the most useful parts of that in about 15 hours. You do not need to be an expert. The goal is to make the chapters feel real, because a service you have configured is far easier to reason about.

> [!warning] These labs use a real AWS account and can cost money
> - Do [[#Lab 0 Set up a safe AWS account|Lab 0]] first, so that you get an alert before spending much.
> - Follow **Clean up** at the end of each lab. Most surprise bills come from things left running, especially NAT gateways, load balancers and databases.
> - AWS's free offer has changed over time. Check the current terms on the [AWS Free Tier page](https://aws.amazon.com/free/).
> - Costs below are rough guides. Check the pricing page for your Region.
> - The console changes often, so these steps describe what to do, and they may not match every button name.

**Work in one Region** for all labs, and use one that is close to you. Start each lab with a clear head: read the steps through first, and try to predict what will happen.

| Lab | Chapters | Time | Rough cost |
| --- | --- | --- | --- |
| 0. Safe account | 01, 02 | 30 minutes | Free |
| 1. IAM | 02 | 1 hour | Free |
| 2. Load balancer and scaling | 04, 05 | 2 hours | Under $1 if cleaned up |
| 3. S3 | 06, 07 | 1 hour | Almost free |
| 4. VPC | 09 | 2 hours | Under $1 if cleaned up |
| 5. CloudFront | 11, 12 | 1 hour | Almost free |
| 6. Databases | 13, 14 | 1.5 hours | Under $1 if cleaned up |
| 7. Serverless API | 16, 17 | 1.5 hours | Almost free |
| 8. Fan-out | 20 | 1 hour | Almost free |
| 9. Encryption and audit | 23, 25 | 1.5 hours | Small, delete the key |
| 10. CloudFormation | 26, 29 | 1 hour | Almost free |

## Lab 0 Set up a safe AWS account

**Goal:** an account that cannot surprise you.

1. Create an AWS account, or use a personal one. Do not use a work account.
2. Sign in as the root user, and **enable MFA** on it. Do not create root access keys.
3. Open **Budgets** and create a monthly cost budget of a small amount, such as $10. Add an email alert at 80% of actual spend and at 100% of forecasted spend.
4. In **Billing preferences**, turn on the billing alerts and free tier usage alerts.
5. Open **IAM Identity Center**, enable it as an organization instance (account instances do not support permission sets), create a user for yourself, and assign the `AdministratorAccess` permission set to your account. If you prefer something simpler for labs, create an IAM user with MFA.
6. Sign out of root, and sign in with the new user. Use this user for all labs.

**Check yourself:** why should you not use the root user for daily work? Which budget alert warned you before you spent the money?

**Clean up:** nothing. Keep the budget.

## Lab 1 IAM roles and least privilege

**Goal:** see policy evaluation and roles working.

1. Create an S3 bucket with a unique name, and upload a small text file.
2. Create an IAM policy that allows `s3:ListBucket` on the bucket ARN, and `s3:GetObject` on `bucket/*`.
3. Create an IAM role for EC2. Attach that policy, plus the AWS managed policy `AmazonSSMManagedInstanceCore`, so that you can connect without SSH.
4. Launch a `t3.micro` or `t4g.micro` Amazon Linux instance with **no key pair**, and attach the role as an instance profile.
5. Connect with **Session Manager**. If it is not available at first, wait a few minutes. The instance needs a route to the internet, or VPC endpoints, to reach Systems Manager, so use a public subnet in the default VPC for this lab.
6. Run `aws s3 ls s3://YOUR-BUCKET` and `aws s3 cp s3://YOUR-BUCKET/file.txt -`. Both should work with no keys on the instance.
7. Try `aws s3 rm s3://YOUR-BUCKET/file.txt`. It should fail with `AccessDenied`.
8. Add an explicit `Deny` for `s3:GetObject` to the role, and test again. Remove it afterwards.
9. Open **IAM Access Analyzer**, and look at how findings are presented. Check the **Last Accessed** tab on your role.

**Check yourself:** where did the credentials come from? Why did the explicit deny win? Why are there two ARNs in the policy?

**Clean up:** terminate the instance. Keep the role, because Lab 2 uses it.

## Lab 2 Load balancer and Auto Scaling

**Goal:** build the standard elastic web tier. Use the default VPC, so that instances can reach the internet to install software.

1. Create a security group for a load balancer that allows HTTP from anywhere.
2. Create a security group for instances that allows HTTP only from the load balancer's security group. Allow no SSH.
3. Create a **launch template** using Amazon Linux, with the role from Lab 1 as its instance profile, and this user data:

   ```bash
   #!/bin/bash
   dnf install -y httpd
   echo "Hello from $(hostname -f)" > /var/www/html/index.html
   systemctl enable --now httpd
   ```

4. Create a **target group** for instances, with an HTTP health check on `/`.
5. Create an internet-facing **Application Load Balancer** across at least two AZs, with a listener that forwards to the target group.
6. Create an **Auto Scaling group** from the launch template across the same AZs, with minimum 2, desired 2 and maximum 4, attached to the target group. Turn on **ELB health checks**.
7. Open the load balancer's DNS name and refresh. The hostname should change between instances.
8. Add a **target tracking** policy on average CPU at 50%.
9. Terminate one instance by hand, and watch the group replace it.
10. Stop the web server through Session Manager (`sudo systemctl stop httpd`) and watch the target become unhealthy and get replaced. This shows why ELB health checks matter.

**Check yourself:** what happens if you turn off the ELB health check type? Why can't anyone reach the instances directly?

**Clean up:** delete the Auto Scaling group first, then the load balancer, target group and launch template. Delete the role from Lab 1.

## Lab 3 S3 versioning and lifecycle

**Goal:** see storage classes, versioning, replication and policies in action.

1. Create a bucket, and leave Block Public Access on.
2. **Enable versioning.** Upload a file, change it, and upload it again. Turn on **List versions**, and find both.
3. Delete the object, and find the delete marker. Delete the marker to restore the object.
4. Add a **lifecycle rule**: move current versions to Standard-IA after 30 days, expire noncurrent versions after 60 days, and delete incomplete multipart uploads after 7 days.
5. Add a **bucket policy** that denies all requests where `aws:SecureTransport` is false. See the example in [[07 S3 Security and Data Protection#Bucket policy examples|the S3 security chapter]].
6. Upload an object with **SSE-KMS**, and look at the object's encryption details.
7. Generate a **presigned URL** for a private object, using `aws s3 presign s3://BUCKET/file.txt --expires-in 300`, or in the console. Open it in a private window, then try the plain object URL, which should fail.
8. Optional: create a second bucket in another Region with versioning on, add a replication rule, and upload a new object. Note that existing objects do not appear.

**Check yourself:** what did the delete marker do? Why does the presigned URL work when the object is private?

**Clean up:** empty the buckets, including all versions, and delete them.

## Lab 4 Build a VPC from scratch

**Goal:** understand every networking component by creating it by hand. Do not use the "VPC and more" wizard.

1. Create a VPC with CIDR `10.0.0.0/16`.
2. Create four subnets: public `10.0.1.0/24` and `10.0.2.0/24`, and private `10.0.11.0/24` and `10.0.12.0/24`, in two AZs. How many usable addresses does each have?
3. Create an **internet gateway**, and attach it.
4. Create a **public route table** with `0.0.0.0/0` to the internet gateway, and associate the public subnets.
5. Launch an instance in a public subnet with a public IP. Allow HTTP. Confirm that you can reach it.
6. Launch an instance in a private subnet, and connect to it using Session Manager if you can. Otherwise, reach it from the public instance. Try `curl https://aws.amazon.com`. It should fail.
7. Create a **NAT gateway** in a public subnet. Add a route `0.0.0.0/0` to it in a private route table, and associate the private subnets. The `curl` should now work.
8. Create an **S3 gateway endpoint**, and add it to the private route table. Look at the new prefix list route.
9. Create a **custom network ACL** on the public subnet. Allow inbound HTTP only, and test. It should fail, because the response is blocked. Add an outbound rule for ports 1024 to 65535, and test again.
10. Turn on **VPC Flow Logs** to CloudWatch Logs, and look for ACCEPT and REJECT records.

**Check yourself:** what makes a subnet public? Why did the NACL need an outbound rule, when the security group did not?

**Clean up:** **Delete the NAT gateway straight away**, because it is charged by the hour. Release its Elastic IP. Terminate instances, delete the endpoint, and delete the VPC.

## Lab 5 Private S3 site behind CloudFront

**Goal:** serve content globally from a private bucket.

1. Create a bucket, and keep Block Public Access on. Upload an `index.html`.
2. Create a **CloudFront distribution** with the bucket as origin, and create an **Origin Access Control**.
3. Set the default root object to `index.html`, and apply the bucket policy that CloudFront offers.
4. Wait for deployment, and open the CloudFront domain name.
5. Try the S3 object URL directly. It should be denied.
6. Change the file, and upload it again. Reload the CloudFront URL, and note that you still see the old copy.
7. Create an **invalidation** for `/index.html`, and reload.
8. Optional: add a **geo restriction** that blocks your own country, and see what happens. Then remove it.
9. If you own a domain, add a Route 53 **Alias** record that points to the distribution, with an ACM certificate in us-east-1.

**Check yourself:** why is the bucket safe? Why was the old content served after the update?

**Clean up:** disable and delete the distribution, then empty and delete the bucket.

## Lab 6 DynamoDB and a read replica

**Goal:** compare a NoSQL table and a relational database.

1. Create a DynamoDB table `Orders`, with partition key `customerId` and sort key `orderId`, using on-demand capacity.
2. Add items with different attributes, and see that the schema is flexible.
3. Run a **Query** for one customer, and a **Scan** with a filter. Compare the capacity consumed.
4. Add a **GSI** with partition key `status`, then query it.
5. Enable **TTL** on an attribute named `expiresAt`.
6. Enable **DynamoDB Streams**, and look at the record format.
7. Optional, and small cost: create a small **RDS PostgreSQL** instance in private subnets, with Single-AZ.
8. Create a **read replica**, and see that it has its own endpoint.
9. Take a manual **snapshot**. See that restoring it would create a new database.
10. Look at the option to convert to Multi-AZ, and read what it says it will do. You do not need to apply it.

**Check yourself:** why was Scan more expensive than Query? Why couldn't you add an LSI to the table now? What is different about the replica's endpoint and a Multi-AZ standby?

**Clean up:** delete the DynamoDB table. Delete the replica, then the database, skipping the final snapshot, and then delete the manual snapshot.

## Lab 7 Serverless API

**Goal:** build the standard serverless chain.

1. Create a DynamoDB table `Items`, with partition key `id`.
2. Create a Lambda function in Python, with an execution role allowing `dynamodb:PutItem` and `dynamodb:GetItem` on that table.

   ```python
   import json, os, boto3, uuid

   table = boto3.resource("dynamodb").Table(os.environ["TABLE_NAME"])

   def lambda_handler(event, context):
       if event.get("requestContext", {}).get("http", {}).get("method") == "POST":
           item = {"id": str(uuid.uuid4()), "text": event.get("body", "")}
           table.put_item(Item=item)
           return {"statusCode": 201, "body": json.dumps(item)}
       item_id = (event.get("queryStringParameters") or {}).get("id", "")
       result = table.get_item(Key={"id": item_id})
       return {"statusCode": 200, "body": json.dumps(result.get("Item", {}))}
   ```

3. Set the environment variable `TABLE_NAME`.
4. Create an **HTTP API** in API Gateway with a Lambda integration, and routes `GET /items` and `POST /items`.
5. Use `curl` to create an item, then fetch it by ID.
6. Remove the DynamoDB permission, and see the error in CloudWatch Logs. Put it back.
7. Change memory and timeout, and see the effect on the duration in the logs.
8. Add **reserved concurrency** of 1, and call the function rapidly. Look for throttles. Then remove it.

**Check yourself:** what did the execution role do? Where do the logs go? What is the difference between reserved and provisioned concurrency?

**Clean up:** delete the API, function, log group, role and table.

## Lab 8 Fan-out with SNS and SQS

**Goal:** see decoupling work.

1. Create an **SNS topic** `orders`.
2. Create two **SQS queues**, `billing` and `shipping`, and a dead-letter queue `orders-dlq`.
3. Subscribe both queues to the topic. Confirm that the queue access policies allow SNS to send.
4. Publish a message to the topic, and look in both queues for a copy.
5. On `billing`, set the DLQ with `maxReceiveCount` of 2.
6. Receive a message twice without deleting it, waiting for the visibility timeout each time. On the next receive attempt, its receive count passes `maxReceiveCount`, and SQS moves it to the DLQ.
7. Change the visibility timeout, and see how long a received message stays hidden.
8. Add a **filter policy** so that `shipping` only gets messages with the attribute `type` equal to `physical`. Publish with and without that attribute.
9. Create a Lambda function with `billing` as an **event source**, and see the queue empty as the function processes messages.

**Check yourself:** why do both queues get a copy? What would happen if a subscriber were HTTP, and it was down? What does the DLQ give you?

**Clean up:** delete the queues, topic and function.

## Lab 9 Encryption and audit

**Goal:** see who did what, and control keys.

1. Create a **customer managed KMS key**. Enable automatic rotation, and look at the default key policy.
2. Encrypt a test object in S3 using the key. Then find the `GenerateDataKey` event in **CloudTrail event history**. This usually appears within a few minutes.
3. In CloudTrail, find the event for creating the key, and note the identity and the time.
4. Create a **secret** in Secrets Manager, and fetch it with `aws secretsmanager get-secret-value`.
5. Create a **SecureString** in Parameter Store, and fetch it with `aws ssm get-parameter --with-decryption`. Compare the two services.
6. Create a **CloudWatch alarm** on a metric, such as EC2 CPU on a test instance, with an SNS email action.
7. Turn on **AWS Config** for a short time, add the managed rule `s3-bucket-public-read-prohibited`, and look at the results. Config charges per item recorded, so turn it off afterwards.
8. Look at the **GuardDuty** console. It has a free trial, and it can generate sample findings.

**Check yourself:** which service told you who used the key? Why does Config detect but not prevent? How do Secrets Manager and Parameter Store differ?

**Clean up:** schedule the KMS key for deletion, using the minimum 7-day wait. Delete the secret, turn off Config recording and delete its rule, and turn off GuardDuty if you enabled it.

## Lab 10 Infrastructure as code and a budget

**Goal:** treat infrastructure as code, and see the cost tools.

1. Save this template as `lab.yaml`:

   ```yaml
   AWSTemplateFormatVersion: "2010-09-09"
   Description: Lab bucket
   Parameters:
     Env:
       Type: String
       Default: dev
   Resources:
     LabBucket:
       Type: AWS::S3::Bucket
       DeletionPolicy: Delete
       Properties:
         VersioningConfiguration:
           Status: Enabled
         Tags:
           - Key: Env
             Value: !Ref Env
   Outputs:
     BucketName:
       Value: !Ref LabBucket
   ```

2. Create a stack from it in **CloudFormation**, and look at the **Events** and **Resources** tabs.
3. Change the tag value by updating the parameter, using a **change set**. Review it before you execute it.
4. Change the bucket's tags by hand in the S3 console, then run **drift detection**.
5. Add a second resource that has an error, and watch the **rollback**.
6. Open **Cost Explorer**. It can take a while to populate on a new account. Group costs by service.
7. Activate a **cost allocation tag** in the Billing console, such as `Env`.
8. Open **Trusted Advisor**, and look at which checks your support plan shows.

**Check yourself:** why is a change set useful? What happens when a stack is deleted if `DeletionPolicy` is `Retain`?

**Clean up:** delete the stack. Remove any leftovers.

## After the labs

Open **Cost Explorer** and **Billing**, and check that nothing is still running. Check every Region that you used. Look for:

- [ ] EC2 instances
- [ ] Load balancers
- [ ] NAT gateways
- [ ] Elastic IPs
- [ ] RDS databases and snapshots
- [ ] EBS volumes and snapshots
- [ ] KMS keys

---
**Plan:** [[Study Guide]]
