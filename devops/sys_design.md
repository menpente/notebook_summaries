This briefing document outlines the fundamental concepts covered in the System Design Crash Course, providing an essential roadmap for understanding scalable and reliable distributed systems.

***

# System Design Crash Course Briefing

## I. Overview and Approach

The System Design Crash Course is designed to demystify system design and provide bite-sized explanations of key ideas, helping beginners grasp fundamental concepts quickly. System design is the process of defining the architecture, components, and data flow of a software system to meet specific requirements.

### The System Design Master Template

Before diving into individual concepts, it is helpful to use a roadmap. The **System Design Master Template** is a blueprint of standard components and steps that should be considered when tackling any design problem. By following this template, you can systematically address requirements, outline architecture, and ensure critical areas like scalability, reliability, and performance are discussed.

Key building blocks included in the template cover:
*   **Load balancers**.
*   **Caches**.
*   **Databases**.
*   **Data partitioning**.
*   **Message queues**.
*   **Microservices architecture**.

***

## II. Core System Design Concepts (20 Essentials)

### 1. Load Balancer

A **load balancer** (hardware or software) distributes incoming traffic across multiple servers. It acts as a smart traffic cop, ensuring no single server is overwhelmed, thus improving performance and preventing downtime. Load balancers employ algorithms (e.g., Round Robin, Least Connections) and perform health checks, stopping traffic to failed servers to maintain high availability.

### 2. Data Partitioning

**Data partitioning** involves splitting a large dataset into smaller parts so each can be managed separately. This improves performance and scalability by allowing queries to target only one partition.
*   **Horizontal partitioning (sharding)** splits data rows across multiple databases.
*   **Vertical partitioning** splits data by columns (grouping certain attributes).
The goal is to distribute load and storage to prevent a single database from becoming a bottleneck.

### 3. Sharding

**Sharding** is a specific type of horizontal data partitioning where a database is broken into smaller pieces called *shards*, each on a different server. Sharding is used when a single database cannot handle the massive scale. A critical decision is choosing a **shard key** (e.g., user ID) to ensure data is evenly distributed and to avoid hot spots.

### 4. CAP Theorem

The **CAP Theorem** describes a fundamental trade-off in distributed systems concerning three qualities in the presence of a network partition (P):
*   **Consistency (C):** All nodes see the same data at the same time (latest write).
*   **Availability (A):** Every request receives a non-error response, though it may not contain the latest write.
*   **Partition Tolerance (P):** The system continues to work despite network breakdowns.

A distributed system can only guarantee two out of the three simultaneously. For instance, many NoSQL databases prioritize A over C ("AP" systems), while some relational databases prioritize C over A ("CP" systems) during a fault.

### 5. CDN (Content Delivery Network)

A **CDN** is a globally distributed network of servers that delivers content (images, videos, web pages) to users from the nearest location. This significantly reduces **latency** (delay users experience). CDNs cache popular content at the edges, reducing load on origin servers, improving reliability, and protecting against traffic spikes.

### 6. Message Queue

A **message queue** uses a queue data structure for sending and receiving messages between services. This mechanism **decouples** the producer (sender) from the consumer (receiver). Message queues enable **asynchronous processing**, helping to smooth out traffic spikes and ensuring resilience, as messages stay in the queue until processed, even if a receiver is down.

### 7. Message Broker

A **message broker** manages and routes messages between different parts of an application. While the queue is the data structure, the broker is the software that organizes queues, handles routing logic, and offers features like persistence and publish/subscribe (pub/sub) patterns. Using a broker (like Apache Kafka) improves **scalability** and **fault tolerance** by achieving loose coupling between services.

### 8. API (Application Programming Interface)

An **API** is a set of rules allowing different software programs to communicate. It defines how clients interact with the service and how microservices communicate with each other. APIs often use exposed endpoints (URLs) and protocols like HTTP (e.g., RESTful APIs). Good API design requires consistent structure, documentation, and proper versioning.

### 9. Replication

**Replication** means keeping copies of data on multiple machines to increase reliability and improve read performance.
*   **Primary-Replica (Master-Slave):** One primary handles all writes; multiple replicas handle reads and serve as failovers.
*   **Multi-Master (Peer-to-Peer):** Multiple nodes handle writes and sync with each other.

Replication is key for high availability. Decisions must be made regarding **synchronous replication** (strong consistency, slower) vs. **asynchronous replication** (faster, potential risk of slight data loss).

### 10. Microservices Architecture

This approach breaks an application into many small, **independent services**, each focused on a specific feature (e.g., user service) and potentially having its own database. Microservices contrast with monolithic architecture. They allow independent development, scaling, and fault isolation. The trade-off is added complexity in managing many distributed services, networking, and debugging.

### 11. SQL vs NoSQL

The choice between database types depends on system needs.
*   **SQL (Relational):** Uses structured tables, fixed schemas, complex queries (JOINs), and offers **strict consistency** (ACID transactions). Ideal for highly relational data and integrity.
*   **NoSQL (Non-relational):** Diverse types (document, key-value, etc.). Designed for **flexibility** and **horizontal scalability**. Often schemaless and prioritizes availability/partition tolerance (often **eventually consistent**). Useful for big data, evolving requirements, or when the relational model is too limiting.

Modern systems often use a mix of both (polyglot persistence).

### 12. Scalability

**Scalability** is the system's ability to handle increased load by adding resources without redesign.
*   **Vertical Scaling:** Adding more power (CPU, RAM) to a single server. Simpler, but physically limited.
*   **Horizontal Scaling:** Adding more servers to share the load. Key for very large systems, achieved through load balancing and data distribution (sharding).

Horizontal scaling introduces complexity but is essential for massive growth.

### 13. Rate Limiting

**Rate limiting** controls how many requests a client can perform within a given time window. It acts as a speed limit to prevent overwhelming the system and ensures fair resource sharing. Algorithms like Token Bucket and Sliding Window track request counts. Rate limiting improves a system’s robustness by preventing API abuse and ensuring stability.

### 14. Reliability

**Reliability** refers to the system's ability to function correctly and consistently over time—it is about trustworthiness and maintaining data integrity. It is ensured through **fault tolerance** (working despite failures), **consistency** (producing accurate data), and **recovery** (recovering quickly from errors). While related to availability, reliability specifically means the system is doing the *right thing* without errors.

### 15. Availability

**Availability** is about ensuring the system is up and reachable when needed, often measured as a percentage of uptime (e.g., 99.9%). High availability requires minimizing downtime through:
*   **Redundancy:** Having backup components or servers.
*   **Failover Mechanisms:** Automatic switching to healthy backups.
*   **Eliminating Single Points of Failure:** Using multiple distributed services or data centers.

### 16. Caching

**Caching** stores frequently accessed data temporarily in a faster storage layer (like memory). This improves performance and reduces the load on main databases by acting as a shortcut. Types include client-side, server-side (Redis/Memcached), and CDN caching. Key strategies include **cache eviction** (e.g., LRU - Least Recently Used, LFU - Least Frequently Used). Caching introduces the trade-off of complexity and potential cache inconsistency (stale data).

### 17. Latency vs Throughput

These are two core performance measures:
*   **Latency:** The time taken for a * single request* to complete (the delay felt by the user).
*   **Throughput:** The *total number of requests* the system can handle per second (like the width of a highway).

Improving one metric often affects the other (e.g., batching increases throughput but raises latency). The necessary balance depends on the application's use case.

### 18. Forward Proxy vs Reverse Proxy

A **proxy** is a middleman for requests.
*   **Forward Proxy:** Sits in front of the *client* and handles outbound requests, typically used for filtering, security, and caching in corporate networks. It protects clients.
*   **Reverse Proxy:** Sits in front of the *servers* and handles inbound traffic. It routes requests, performs load balancing, handles SSL termination, and hides the backend infrastructure. It protects servers.

### 19. Domain Name System (DNS)

The **DNS** is the internet’s phone book, translating human-friendly domain names (like `google.com`) into machine-readable IP addresses. DNS relies heavily on caching (using Time-To-Live, or TTL, values) to speed up lookups. DNS supports complex architectures, including global load balancing and failover routing.

### 20. Long Polling vs WebSockets

Both enable real-time communication.
*   **Long Polling:** Uses regular HTTP requests that the server holds open until new data is available; the client immediately opens a new request afterward. It is simpler to implement and firewall-friendly.
*   **WebSockets:** Creates a **persistent two-way connection** after an initial handshake, allowing continuous data exchange. This is ideal for instant updates in chat or gaming, as it reduces overhead, but it requires stateful connection management.

***

## III. Key System Design Trade-offs and Considerations

### Addressing Complexity

In interviews, it is crucial to discuss trade-offs openly, as every design decision has pros and cons. Common pitfalls include jumping into design without clarifying requirements and focusing too heavily on one aspect while neglecting failure scenarios or simplicity.

### Load Balancer vs. API Gateway

While both are entry points, they serve different primary roles:
*   **Load Balancer:** Focuses on distributing traffic across multiple identical instances for balancing load and improving reliability.
*   **API Gateway:** Acts as a single entry point for clients to access various microservices, handling routing, authentication, and rate limiting.

In practice, a load balancer often sits in front of multiple API Gateway instances.

### Microservice Communication Patterns

Microservices can communicate in two main ways:
1.  **Synchronously:** Direct requests (e.g., HTTP/REST or gRPC), where Service A calls Service B and waits for a response. This creates tighter coupling.
2.  **Asynchronously:** Using **message brokers/queues**, where Service A publishes an event to a topic, and Service B consumes it independently. This decouples services, improving resilience and supporting event-driven architectures.

---
*By understanding how these core concepts interplay and the trade-offs involved, you can effectively approach designing systems that meet specific requirements for scale and reliability.*
