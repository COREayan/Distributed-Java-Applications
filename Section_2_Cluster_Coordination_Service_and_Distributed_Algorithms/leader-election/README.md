# ⚡ Section 2: Cluster Coordination Service & Distributed Algorithms

---

## 📖 Terminology

### 🔹 Node
- A **process** running on a dedicated machine.

### 🔹 Cluster
- A **collection of computers/nodes** connected to each other.  
- Nodes in a cluster usually:  
  - Work on the same task  
  - Run the same code  

---

## ⚠️ Challenges in Master-Worker Architecture

- Leader election is **non-trivial**, even for humans — much harder in distributed systems.  
- Reaching **agreement** on a leader in a large cluster of nodes is difficult.  
- By default, **each node only knows about itself** → requires **Service Registry & Discovery**.  
- **Failure Detection** is critical to trigger automatic leader re-election.  

---

## 🛠️ Master-Worker Coordination Solutions

- Implement **distributed consensus & failover algorithms** from scratch.  
- Use **Apache Zookeeper** → A **high-performance distributed coordination service**.  

---

## 🐘 Apache Zookeeper

- Designed specifically for **distributed systems**.  
- Widely used in production by **Kafka, Hadoop, HBase**, and many more.  
- Provides an **abstraction layer** for higher-level distributed algorithms.  
- **Distributed & fault-tolerant system** itself (ensures high availability & reliability).  
- Typically runs in a **cluster of an odd number of nodes (≥ 3)**.  
- Uses **redundancy** to allow failures while staying functional.  

---

## 📂 Znodes

### 🔹 Properties
- **Hybrid of File + Directory**  
  - Can **store data** (like a file).  
  - Can have **children znodes** (like a directory).  

### 🔹 Types
- **Persistent** → Remains available between sessions.  
- **Ephemeral** → Exists only while the session is active; removed when session ends.  

---

## 🔄 Zookeeper Threading Model

- Application code starts on the **Main Thread**.  
- When a **Zookeeper object** is created → 2 additional threads start:  
  1. **IO Thread**  
  2. **Event Thread**  

### ⚡ IO Thread
- Handles **network communication** with Zookeeper servers.  
- Processes **requests & responses**.  
- Manages **pings, sessions, and timeouts**.  

### ⚡ Event Thread
- Manages **Zookeeper events**, such as:  
  - **Connection events** (e.g., `SyncConnected`)  
  - **Disconnection events**  
- Executes **custom Znode watchers & triggers** in **order**.  

---
