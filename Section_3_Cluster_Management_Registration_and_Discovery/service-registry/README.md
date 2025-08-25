## 🚀 Section 3 : Cluster Management, Registration and Discovery

---

### ⚙️ Static Configuration vs Dynamic Configuration

- Some companies still manage their clusters in a **static way**, with limited automation.
- In **dynamic configuration**, every time a new node is added, a central configuration is updated.
- Tools like **Chef** or **Puppet** can pick up the configuration automatically and distribute it among all nodes in the cluster.

---

### 👑 Leader / 🛠️ Workers Architecture

- **Workers** will register themselves with the cluster.
- Only the **Leader** registers for notifications.
- The **Leader** always knows the state of the cluster and distributes work accordingly.
- If a **Leader** fails, the **new Leader** removes the old entry from the service registry and continues distributing the work.

---

### 📦 Storing Configuration / Address

- Configuration data can be stored inside a **znode**.
- Only the **minimum data** needed for cluster communication should be stored.
- Example address format:
  - Host Name : Port example: http://127.0.0.1:8080

