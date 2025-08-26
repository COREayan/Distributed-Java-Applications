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
