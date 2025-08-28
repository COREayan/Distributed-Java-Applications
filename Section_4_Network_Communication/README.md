# 🌐 Section 4 : Network Communication

---

## 🔗 Layer 1 - Data Link  
**Physical delivery of data over a single link.**  
Responsible for:  
- 📦 Encapsulation of the data  
- 🔄 Flow control  
- ⚠️ Error Detection  
- ✅ Error Correction  
- … and more  

---

## 🌍 Layer 2 - Internet  

---

## 🚚 Layer 3 - Transport  

### ✉️ User Datagram Protocol (UDP)  
- ⚡ Connectionless  
- 🎲 Best effort — Unreliable  
  - Messages can be **Lost**, **Duplicated**, **Reordered**  
- 📦 Based on a unit called **Datagram** (limited in size)  

**UDP in Distributed Systems**  
- Preferred when **speed** & **simplicity** > reliability  

**UDP Use Cases**  
- 📝 Sending debug info to logging service  
- 🎥 Real-time streaming (video/audio)  
- 🎮 Online Gaming  
- 📡 Broadcasting → Decouples sender & receiver(s)  

---

### 🔒 Transmission Control Protocol (TCP)  
- ✅ Reliable — Guarantees data delivery as sent  
- 🔗 Requires a connection  
  - Connection **created** before sending  
  - Connection **closed** after sending  
- 📡 Works as a streaming interface  
- 🌟 Most popular in distributed systems due to reliability  

---

## 🔌 Layer 3.5 - TCP Connection  

---

## 🖥️ Layer 4 - Application  

### 📜 Application Layer Protocols  

| Protocol | Purpose |
|----------|----------|
| 📂 **FTP** (File Transfer Protocol) | Transferring files through the web |
| ✉️ **SMTP** (Simple Mail Transfer Protocol) | Sending and receiving emails |
| 🌐 **DNS** (Domain Name System) | Translating hostnames → IP addresses |
| 📑 **HTTP** (Hypertext Transfer Protocol) | Transmitting documents, video, sound, images |

---

### 🌐 HTTP Request Methods  
- 🔍 GET  
- 📑 HEAD  
- 📨 POST  
- ✏️ PUT  
- ❌ DELETE  
- 🔎 TRACE  
- 🔗 CONNECT  
- ⚙️ OPTIONS  
- 🩹 PATCH  

#### ✅ GET  
1. **Safe** → Retrieval only (like a Java getter)  
2. **Idempotent** → N times = 1 time  

#### 📨 POST  
- Contains a **message body (payload)**  
- May have **side effects**  
- Useful for **complex operations** and **node communication**  

---

### 🌐 HTTP Versions  
- HTTP/1.1  
- HTTP/2  

**HTTP/1.1 Drawbacks**  
- 🔄 New connection per request = Expensive  
- ⚠️ Limited outgoing connections  
  - Ports  
  - OS limits  

---

### 📬 HTTP Headers  

**Usage**  
- Provide metadata for actions before reading body  
  - Memory Allocation  
  - Skipping/Forwarding (Proxying)  

**Message Body Information**  
- 📏 `Content-Length` → Size of body  
- 🏷️ `Content-Type` → Type of message  
- 🗜️ `Content-Encoding` → Compression algorithm  

**Custom Headers**  
- 🐞 `X-Debug` → Debug info  
- 🧪 `X-Experiment` → A/B testing features  
- 🧾 `X-Test` → Operate on test data  
- ⏱️ `X-Timestamp` → Instrumentation  

**Protocol Differences**  
- **HTTP/1.1** → Plain text key-value pairs (easy to inspect with Wireshark)  
- **HTTP/2** → Headers compressed  
  - ➕ Saves payload size  
  - ➖ Harder to debug  

---

### 📦 HTTP Message Body  
- Can contain **anything** (client & server must agree)  
- Can include **complex data objects**  

---

### 📊 HTTP Status Codes  

| Status Code | Group |
|-------------|--------|
| 1xx | ℹ️ Informational Response |
| 2xx | ✅ Success |
| 3xx | 🔀 Redirection |
| 4xx | ❌ Client Errors |
| 5xx | ⚡ Server Errors |

# HTTP Server
- The HTTP Server will have two endpoints:
  - /status - Handles Get requests
    - Reports the health of our application
  - /task - Handles Post requests
    - Calculates a product of a list of integers
    - Send the results back to the client.

# cURL - Command Line Http Client
  - Using cURL we can test our HTTP server.
  - Has many features and arguments.
    - --request HTTP_METHOD
    - --header HEADER_LINE
    - --verbose(-v)
    - --data SOME_DATA
    - HTTP Server address

# HTTP Client
- We will use the built HTTP Client implementation which was added in JDK 11.
- There are many other third party implementations for both HTTP client and server.
  - Key Features
    - Support for sending HTTP requests asynchronously.
    - Maintaining a connection pool to all the downstream HTTP servers.

# Connection Pooling
- If HTTP/2 is enabled on both HTTP Server and Client.
  - Connection pooling is enabled by default.
- If one of the peers does not support HTTP/2
  - We need to make sure it's enabled by default.
  - Or enable it explicitly.
- JDK built-in HTTP Client supports
  - HTTP/2 and
  - HTTP 1.1 connection pooling by default.
- In most 3rd party HTTP clients we need to enable connection pooling by setting "Keep Alive" to true.
- JDK Built-in HTTP Server does NOT support HTTP/2 (as of JDK 11).

# Wireshark 
- Package analyzer that allows us to inspect network traffic going in and out of a particular computer.
- The best tool for troubleshooting and debugging of complex networking issues.
- Great tool for learning the internal of the underlying protocols.

# Single App vs a Distributed System 
- Unlike a simple method invocation on a single machine.
- Many things can happen after the client sent a request, that are outside of the client's control.

# Idempotent Operation definition
- An operation that can be performed multiple times, and will have the same result/effect as if it was performed only once.

# Idempotent vs non-idempotent Examples 
- Idempotent operations examples:
  - Read the first line in a file.
  - Update the status of a user to "active"
  - Delete a record by ID
 - Safe to perform using At Least Once semantics.
 - Performing those operations multiple times will yield the same result.
 - Non-idempotent operations examples:
   - Appending a line to a file.
   - Incrementing a metric in a database.
   - Withdrawing money from a user's account.
  - Unsafe to perform using At Least Once semantics.
  - Performing those operations more than once will have adverse and undesired effect on the system.

# What to do when an operation is not idempotent? 
- Our operation is not idempotent.
- Losing the operation is out of the question.
- Then we have to make the non-idempotent operation, idempotent artificially.

Note on non-idempotent operations
- Making some non-idempotent operations, idempotent is hard.
- Sometimes making a non-idempotent operation, idempotent is impossible and we need to rethink the system design.
- This is a price we pay for a loosely coupled and scalable distributed system.

# Serialization & Deserialization
- Serialization - Translation of a data structure or object into a format that can be sent (or stored somewhere) and reconstructed later.
- Deserialization - Reconstruction of the data back to a data structure or an object.

# Serialization Formats 
- JSON - JavaScript Object Notation
- Java Object Serialization
- Google's Protocol Buffers

# JSON - JavaScript Object Notation 
- One of simplest and most popular formats
- We can represent an object in plain text with fields of type:
  - String
  - Number(int/float)
  - Boolean
  - Array
  - Objects
- Advantages
    - Simple and human readable
      - Even after serialization we can understand it an debug it.
      - It's plain text so we can create the object and send it(using cURL for example) without any special software.
     - Programming language independent
       - We can have one node written in Java, talking to another node written in C++ for example.
     - Easy integration with JavaScript/Front-End
       - JavaScript Object NOtation is very similar to JavaScript Object representation.
- Disadvantages
  - Java does not know how to map a Java class to/from Json Object.
    - Requires explicit serialization and deserialization using external libraries.
    - Those libraries need explicit configurations and annotation to tell them how to serialize and name the fields.
  - Json does not have a schema(source of truth)

# Data Serialization Formats in Java

## JSON  
### Disadvantages (No Schema)
- Requires explicit serialization and deserialization
  - Often requires external libraries  
  - Those libraries need explicit configurations and annotations to define field serialization
- JSON does not have a schema (source of truth)
- Plain text parsing and transmission is suboptimal  

---

## Serializable Interface in Java
- `Serializable` is an empty **marker interface**
- Objects of classes implementing `Serializable` can be:
  - Serialized into a byte stream  
  - Reconstructed into the original object’s state  
- All members are serialized **except**:
  - Static members  
  - Transient members  

---

## Java Object Deserialization
- The class definition must match the original class
- The class must have an **accessible no-args constructor**
- If either condition fails → `InvalidClassException` during deserialization  

---

## Java Object Serialization  

### Advantages
1. Guarantees correct state reconstruction without type ambiguity  
2. Provides a clear source of truth (schema) for the object  
3. Native support in all JVM languages  
   - No external libraries required  
   - Simple development process  

### Disadvantages
1. Not human-readable → harder to test  
   - Requires importing the class and writing a Java program to send a message  
2. Tight coupling to JVM languages  
   - Incompatible with cross-platform systems (e.g., GoLang, C++)  
   - Limits distributed systems involving diverse technologies  

---

## Protocol Buffers  

### Advantages
1. No type ambiguity  
2. Clear and well-defined schema  
3. Language independent (via 2-step process)  
   - Proto file definition  
   - Language-specific stub generation using the proto compiler  
4. Efficient serialization & deserialization  
5. Built-in security  

### Disadvantages
- Not human-readable  
- Hard to debug  
- More complex development process  
  - Requires proto file definition  
  - Stub generation step  
