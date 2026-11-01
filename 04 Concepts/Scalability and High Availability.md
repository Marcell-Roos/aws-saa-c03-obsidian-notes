---
tags: [concept, scope/in]
aliases: ["High Availability", "high availability", "horizontal scaling", "vertical scaling", "Elasticity"]
---

# Scalability and High Availability

**Scalability** means that an application or system can handle greater loads by adapting. Scalability is linked but different to High Availability. There are two types of scalability:

- **Vertical Scalability**

    Increasing the size of the instance (**scale up/down**). Example: If we have application that runs on a t2.micro, scaling that application vertically means running it on t2.large.

    Vertical Scalability is very common for non distributed systems, such as a database.

- **Horizontal Scalability (Elasticity)**

    Increasing the number of instances/systems for our application (**scale out/in**). Horizontal scaling implies distributed systems (very common for web applications).

**High Availability** means running our application or system in at least 2 AZ. High Availability usually goes hand in hand with horizontal scaling. The main goal of high availability is to survive data center loss (disaster).

**Scalability vs Elasticity**

- Scalability - ability to accommodate a larger load by making the hardware stronger (scale up) or by adding nodes (scale out).
- Elasticity - once a system is scalable, elasticity means that there will be some “auto-scaling” so that the system can scale based on the load (**automatic horizontal scaling**).

## Exam tasks
- [[Task 2.1 Design scalable and loosely coupled architectures]]

---
**Up:** [[Home]]
