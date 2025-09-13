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

### 👀 Watchers and Triggers
- We can register a watcher when we call the methods.
    - 📂 getChildren(..)
    - 📑 getData(..)
    - 📌 exists(..)
-  The watcher allows us to get a notification when a change happens.
-  getChildren(.., watcher) - Get notified when the list of a znode's children changes.
-  exists(znodePath, watcher) - Get notified if a znode gets deleted or created.
-  getData(znodePath, watcher) - Get notified if a znode's data gets modified.
- ️ `public ZooKeeper(String connectString, int sessionTimeout, Watcher watcher)` - Also takes a watcher.
-  Watchers registered with getChildren(), exists() and getData() are **one-time triggers**.
-  If we want to get future notifications, we need to register the watcher again.

---

### 🐑 The Herd Effect
-  A large number of nodes waiting for an event.
-  When the event happens all nodes get notified and they all wake up.
-  Only one node can "succeed".
- ️ Indicates bad design, can negatively impact the performance and can completely freeze the cluster.

### 📚 Resources

- [🐘 Apache ZooKeeper (Official Site)](https://zookeeper.apache.org/) – Official homepage with downloads, docs, and news.  
- [📘 Apache Wiki: ZooKeeper Index](https://cwiki.apache.org/confluence/display/ZOOKEEPER/Index) – Centralized wiki for community notes and guides.  
- [📄 ZooKeeper Documentation](https://zookeeper.apache.org/doc/current/index.html) – Latest version docs with API references and tutorials.  
- [📈 High Scalability: ZooKeeper](https://highscalability.com/zookeeper-a-reliable-scalable-distributed-coordination-syste/) – Article on ZooKeeper’s reliability and scalability.  
- [🔗 Reintech Blog: Using ZooKeeper in Hadoop](https://reintech.io/blog/using-apache-zookeeper-for-cluster-coordination-in-hadoop) – Practical guide on ZooKeeper for cluster coordination.  
