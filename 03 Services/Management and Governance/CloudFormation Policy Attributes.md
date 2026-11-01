---
tags: [service, cat/management, scope/in]
---

# CloudFormation Policy Attributes

**CreationPolicy** attribute allows us to specify a policy for how [[AWS CloudFormation|CloudFormation]] should handle the creation of a resource. This is often used with resources that need additional time to become fully functional or require validation before they are considered created. We can prevent attribute status from reaching create complete until AWS CloudFormation receives a specified number of success signals or the timeout period is exceeded. To signal a resource, we can use the cfn-signal helper script or SignalResource API.

```json
Resources:
  MyInstance:
    Type: AWS::EC2::Instance
    CreationPolicy:
      ResourceSignal:
        Count: 1
        Timeout: PT15M
```

**DependsOn** attribute specifies that the creation of one resource depends on the creation of another resource. This is useful when you need to control the order in which resources are created or updated.

```yaml
Resources:
  MyBucket:
    Type: AWS::S3::Bucket

  MyBucketPolicy:
    Type: AWS::S3::BucketPolicy
    DependsOn: MyBucket
```

**UpdatePolicy** attribute defines how CloudFormation should handle updates to a resource. This is useful for managing rolling updates or handling update failures for certain resources.

```yaml
Resources:
  MyAutoScalingGroup:
    Type: AWS::AutoScaling::AutoScalingGroup
    UpdatePolicy:
      AutoScalingRollingUpdate:
        MinInstancesInService: 1
        MaxBatchSize: 1
        PauseTime: PT5M
```

**UpdateReplacePolicy** attribute specifies what CloudFormation should do with a resource when it is replaced during an update. This is useful for controlling the behavior of resources like [[Amazon RDS|RDS]] instances or [[Amazon S3|S3 buckets]] when they are replaced.

```yaml
Resources:
  MyBucket:
    Type: AWS::S3::Bucket
    UpdateReplacePolicy: Retain
```

---
**Up:** [[AWS CloudFormation]] · **Map:** [[Management and Governance Map]]
