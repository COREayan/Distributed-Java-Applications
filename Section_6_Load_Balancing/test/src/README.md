## Section 6: Load Balancing

### Load Balancers
- Distributes network traffic across a cluster of application servers.
- Prevents any single application server from being a performance bottleneck.
- Monitors application servers' health, load balancers make our system more reliable.

### Cloud Auto-Scaling with load balancers
- In a cloud environment machines can be added on demand.
- A load balancer can provide auto scaling/down scaling capabilities.

### Types of Load Balancers
- Hardware Load Balancers - dedicated hardware devices designed and optimized for the load balancing.
  - High performance
  - Can balance the load to larger number of servers
  - More reliable
- Software Load Balancers - load balancing software
  - Easy to configure, update, upgrade or troubleshoot.
  - Cheaper and more cost effective
  - Open source solutions are available(HAProxy, Nginx)

### 1. Round Robin

### 2. Weighted Round Robin

### 3. Source IP Hash Motivation
- Sometimes it's desired that the user continues communication with the same server.
- Examples:
  - Open Session - Maintaining online shopping cart state between connection loses or browser refresh
  - Local Server Caching - Improving performance by 
    - Preloading data
    - Caching data locally
- Requests from the same user should go to the same server throughout the entire session.

### Drawbacks of Statistical Load Balancing
- We assumed that spreading the requests evenly would also spread the load evenly.
- However: 
  - Not all users are using the system the same way
  - Not all requests require the same amount of resources
- Getting the load balancing strategy wrong can have a cascading chain of failures

### Different Load on Servers Problem
- Neither of the strategies we mentioned took the actual load on the servers into account
- If we have a range of resources requirements between different requests
- The solution is to take a more active approach to monitoring servers' load

### 4. Least Connections

### 5. Weighted Response Time

### 6. Agent Based Policy Metrics
- CPU Utilization
- Inbound or outbound Network Traffic(bytes)
- Disk Operations(Reads/Writes)
- Memory Utilization
- Others...

### Load Balancing Layers
- Transport Layer Load Balancing
  - Layer 4 in the OSI Model
- Application Layer Load Balancing
  - Layer 7 in the OSI Model

### Layer 4 (Transport) Load Balancing
- The Load Balancer performs simple TCP packets forwarding between the client and the backend servers.
- Does not inspect the content of the TCP stream beyond the first few packets - Low overhead

### Layer 7 (Application) Load Balancing
- Can make smarter routing decisions based on the HTTP header
- Load balancer inspects TCP packets and HTTP header
- Can route requests to different clusters of servers based on:
  - Request URL
  - Type of requested data
  - HTTP method
  - Browser cookies
- 