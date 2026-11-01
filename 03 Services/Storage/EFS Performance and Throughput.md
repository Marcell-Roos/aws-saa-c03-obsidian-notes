---
tags: [service, cat/storage, scope/in]
---

# EFS Performance and Throughput

**Performance Classes**

- **Performance Mode**
    - **General Purpose (default)** - best for latency-sensitive applications, such as web serving, content management systems, and development environments.
    - **Max I/O** - historically for highly parallel workloads, but it has higher latency and AWS now recommends always using General Purpose.
- **Throughput Mode**
    - **Bursting Throughput** - throughput scales with the size of the file system. Suitable for most file systems, offering a balance between cost and performance.
    - **Provisioned Throughput** - allows us to specify the desired throughput level, which can exceed what is available via the burst mode. Best for applications requiring a consistent and predictable level of throughput.
    - **Elastic Throughput** - automatically scales up or down based on our workloads. Best for unpredictable workloads.

## Exam tasks
- [[Task 3.1 Determine high-performing and or or scalable storage solutions]]

---
**Up:** [[Amazon EFS]] · **Map:** [[Storage Map]]
