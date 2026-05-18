# 🌐 Foundational Topics in System Design - I

This document provides an engineering overview of the core architectural components that form the bedrock of scalable distributed systems.

---

## 🚀 1. Content Delivery Network (CDN)
A **CDN** is a globally distributed network of proxy servers and data centers designed to provide high availability and performance by distributing spatial content closer to end-users.

* **How it Works:** Instead of hitting the origin server for every asset, user requests are routed to the nearest **Edge Server** (Point of Presence - PoP). 
* **Caching:** It caches static resources (HTML, CSS, JavaScript, Images, Videos) based on TTL (Time-To-Live) configurations.
* **Benefits:** Reduces latency, minimizes origin bandwidth consumption, handles traffic spikes gracefully, and provides DDoS mitigation.
* **Reference:** [Cloudflare - What is a CDN?](https://www.cloudflare.com/en-in/learning/cdn/what-is-a-cdn/)

---

## 🗄️ 2. Key-Value (KV) Stores
A **Key-Value Database** is a type of non-tabular (NoSQL) storage that uses an associative array as its fundamental data model, where each unique key is mapped to exactly one value.

* **Characteristics:** Highly partitioned, optimized for simple read/write patterns, and supports extreme horizontal scaling (sharding) because data lacks complex structural dependencies.
* **Performance:** Provides $O(1)$ constant-time lookups.
* **Limitations:** Does not natively support complex relational queries, multi-table joins, or secondary filtering on nested fields without building custom auxiliary tables or indexes.
* **Examples:** Redis, Aerospike, Amazon DynamoDB.
* **Reference:** [Wikipedia - Key-Value Database](https://en.wikipedia.org/wiki/Key%E2%80%93value_database)

---

## ⚡ 3. WebSockets
**WebSockets** provide a persistent, full-duplex, bidirectional communication channel over a single long-lived TCP connection between a client and a server.

* **The Connection Lifecycle:** Initiated via an HTTP request containing an `Upgrade` header. Once the handshake succeeds, the protocol switches from HTTP to WebSocket (`ws://` or `wss://`).
* **Comparison with HTTP:** Unlike traditional HTTP polling where the client must explicitly initiate every request, WebSockets allow either party to push data instantly without protocol overhead (headers) on every frame.
* **Ideal Use Cases:** Real-time chat applications, live financial tickers, collaborative editors, multiplayer gaming, and push notification delivery systems.
* **Reference:** [Twilio - What are WebSockets?](https://www.twilio.com/docs/glossary/what-are-websockets)

---

## ⚖️ 4. Load Balancers
A **Load Balancer** acts as a reverse proxy, distributing incoming network traffic across a healthy cluster of backend application servers to maximize throughput, optimize utilization, and prevent bottlenecks.

* **Core Operational Duties:**
  1. Terminates incoming connections from the client.
  2. Evaluates structural availability via an internal registry.
  3. Uses routing algorithms (e.g., Round Robin, Least Connections, IP Hashing) to select a destination node.
  4. Forwards the payload and transparently pipes the response back.
* **Redundancy:** Removes single points of failure by automatically rerouting traffic away from degraded or unresponsive servers.
* **Reference:** [DigitalOcean - What is Load Balancing?](https://www.digitalocean.com/community/tutorials/what-is-load-balancing)

---

## 🚌 5. Message Brokers
A **Message Broker** is an intermediary architectural component that translates messages between decoupled services using a formal communication protocol, validating asynchronous workflows.

* **Structural Models:**
  * **Point-to-Point (Queues):** A producer puts a message in a queue, and exactly one consumer processes it before it is purged (e.g., AWS SQS).
  * **Publish/Subscribe (Event Bus):** A producer publishes an event to a topic, and multiple independent subscribers consume that exact same copy concurrently at their own pace (e.g., Apache Kafka, RabbitMQ).
* **Engineering Advantages:** Guarantees temporal decoupling, absorbs sudden ingestion spikes (load-leveling), and scales consumers independently.
* **Reference:** [TSH Blog - Message Broker](https://tsh.io/blog/message-broker/)

---

## 💓 6. Heartbeats in Distributed Systems
In distributed infrastructure, a **Heartbeat** is an auxiliary message sent at uniform periodic intervals ($t$) from a node to a central monitor, supervisor, or cluster peer to state its current health and operational status.

* **Failure Detection:** If a supervisor node fails to receive a configuration-defined number of continuous heartbeat slots, it marks the target node as "Dead" or unavailable.
* **Cluster Repercussions:** Triggers infrastructure workflows, including orchestrator node evictions, failovers, dynamic load balancer route adjustments, or initiating a new consensus **Leader Election** term.
* **Reference:** [Wikipedia - Heartbeat (Computing)](https://en.wikipedia.org/wiki/Heartbeat_(computing))

---

## 🏛️ 7. Designing a Good Database Schema
A robust database schema design establishes structural blueprints, enforcement rules, and relational boundaries governing how application domain objects are stored, mutated, and queried.

* **Core Principles:**
  * **Normalization:** Organizes columns and tables to eliminate data redundancy and prevent anomalies (Insertion, Update, Deletion) while guaranteeing data integrity.
  * **Denormalization Trade-offs:** Intentionally introducing redundancy in read-heavy NoSQL systems to bypass expensive runtime queries and merge cycles.
  * **Index Strategies:** Designing appropriate primary keys, foreign keys, and compound secondary indexes to maximize search throughput while balancing write overhead.
  * **Reference:** [Medium - Relational Database Schema Design Overview](https://medium.com/@kimtnguyen/relational-database-schema-design-overview-70e447ff66f9)

---
