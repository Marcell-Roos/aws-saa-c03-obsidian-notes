---
tags: [service, cat/application, scope/in]
---

# Step Functions Map State

**[[AWS Step Functions]]' Map State** is a feature designed to iterate over a collection of items and process each one in parallel or sequentially, depending on how we configure it. It allows us to specify a JSON array (or list) as input and then iterate over that array and apply a specified state machine (or sub-state machine) to each item.

The Map state allows us to configure how many iterations are processed in parallel. We can set a MaxConcurrency value to limit the number of parallel executions.

**Inline mode:** runs iterations inside the parent execution, for smaller collections.

```json
{
  "Type": "Map",
  "ItemsPath": "$.items",
  "MaxConcurrency": 10,
  "ItemProcessor": {
    "ProcessorConfig": { "Mode": "INLINE" },
    "StartAt": "ProcessItem",
    "States": {
      "ProcessItem": {
        "Type": "Task",
        "Resource": "arn:aws:states:::lambda:invoke",
        "Parameters": { "FunctionName": "ProcessItemFunction", "Payload.$": "$" },
        "End": true
      }
    }
  },
  "End": true
}
```

**Distributed mode:** each iteration runs as a separate child workflow execution, for very large parallel jobs such as processing objects in [[Amazon S3|S3]].

```json
{
  "Type": "Map",
  "ItemReader": {
    "Resource": "arn:aws:states:::s3:listObjectsV2",
    "Parameters": { "Bucket": "my-bucket" }
  },
  "ItemProcessor": {
    "ProcessorConfig": { "Mode": "DISTRIBUTED", "ExecutionType": "STANDARD" },
    "StartAt": "ProcessItem",
    "States": {
      "ProcessItem": {
        "Type": "Task",
        "Resource": "arn:aws:states:::lambda:invoke",
        "Parameters": { "FunctionName": "ProcessItemFunction", "Payload.$": "$" },
        "End": true
      }
    }
  },
  "End": true
}
```

The source's distributed example used an invalid `StateMachine` state type, so both examples were rewritten with `ItemProcessor`.

---
**Up:** [[AWS Step Functions]] · **Map:** [[Application Integration Map]]
