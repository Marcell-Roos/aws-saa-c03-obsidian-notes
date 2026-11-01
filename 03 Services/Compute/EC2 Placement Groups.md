---
tags: [service, cat/compute, scope/in]
aliases: ["placement group", "Placement Groups"]
---

# EC2 Placement Groups

**EC2 Placement Groups** are a feature that enables us to influence the placement of [[Amazon EC2]] instances on the underlying hardware. This can be important for workloads that require high performance, low latency, or other specific characteristics.

If we receive a capacity error when launching an instance in a placement group that already has running instances, stop and start all of the instances in the placement group, and try the launch again. Restarting the instances may migrate them to hardware that has capacity for all the instances.

- **Cluster Placement Group**

    Designed for applications that need low network latency, high network throughput, or both and for Big Data jobs that need to complete fast.

    All instances must be in the same AZ and there might be limits on the number of instances we can place in a single group depending on the instance type and available hardware.

- **Spread Placement Group**

    Suited for applications that require [[Scalability and High Availability|high availability]].

    Instances are distributed across distinct underlying hardware. This minimizes the risk of correlated hardware failures. Spread placement groups have stricter limits on the number of instances per AZ, typically up to seven.

- **Partition Placement Group**

    Useful for large-scale distributed and replicated workloads, such as Hadoop, Cassandra, and Kafka.

    Instances are divided into logical partitions, each isolated from the other in terms of failure. Failures in one partition do not affect the instances in other partitions. We have more control over where instances are placed, but the number of partitions and instances per partition can be constrained.

    AWS calls them "logical partitions," but each partition maps to its own set of racks.

| Type | Spread | Use |
| --- | --- | --- |
| Cluster | One AZ, close together | Lowest latency, HPC |
| Spread | Separate racks, 7 per AZ | Critical instances |
| Partition | Up to 7 partitions per AZ | Hadoop, Cassandra, Kafka |

## Exam tasks
- [[Task 3.2 Design high-performing and elastic compute solutions]]

---
**Up:** [[Amazon EC2]] · **Map:** [[Compute Map]]
