## Section 7 : Distributed Message Brokers

1. Synchronous Network Communication 
2. Broadcasting Event to Many Services
3. Traffic Peaks and Valleys

### Message Broker Definition
- Intermediary software(middleware) that passes messages between sender(s) and receiver(s).
- May provide additional capabilities like:
  - Data transformation
  - Validation
  - Queuing
  - Routing
- Full decoupling between sender(s) and receiver(s)

### Message Brokers Scalability
- To avoid the Message Broker from being a single point of failure or a bottleneck
- Message Brokers need to be scalable and fault tolerant
- Message Brokers are distributed systems by themselves, which makes them harder to design and configure
- The latency, when using a message broker, in most cases, is higher than when using direct communication

### Most Popular Use Cases
- Distributed Queue - Message delivery from a single producer to a single consumer
- Publish / Subscribe - Publishing of a message from a single publisher to a group of subscribed consumers

### Apache Kafka
- Distributed Streaming Platform, for exchaning messages between different servers
- Can be described as a Message Broker on a high level
- Internally Kafka is a disributed system that may use multiple message brokers to handle the messages

### Why Learning Apache Kafka
- There are many great message brokers
  - Open Source : **RabbitMQ, ActiveMQ** etc..
  - Proprietary messaging systems offered by the cloud vendors
- **Apache Kafka** is open source and provides:
  - Distributed Queuing
  - Publish/Subscribe
- Beautifully designed Distributed System for high scalability and fault tolerance

### Kafka Scalability through Partitioning
- Kafka Topic partitioning allows us to scale a topic horizontally
- More partitions in a topic -> higher parallelism

### Kafka Brokers & Topic Partitions
- Number of partitions in a topic ~= maximum unit of parallelism for a Kafka Topic
- We can estimate the right number of partitions for a topic given expected our peak message rate/volume
- By adding more message brokers we can increase the Kafka topics capacity, tranparently to the publishers

### Topic Partitions and Parallelism
- Thanks to the partitioning of a Topic
  - We can have many broker instances working in parallel to handle incoming messages
  - And having many consumers, consuming in parallel from the same topic

### Replication - Leader & Followers
- Each Kafka Topic is configured with a replication factor
- A replication factor of N means each partition is replicated by N Kafka brokers
- For each partition, only one broker acts as a partition leader, other brokers are partition followers
- The leader takes all the reads and writes
- The followers replicate the partition data to stay in sync with the leader

### Replication Pros & Cons
- The higher replication factor the more failures our system can tolerate. 
- But more replication means more space is taken away from the system just for redundancy.

### Fault Tolerance Implementation
- The replication is configured on per topic basis
- Kafka tries its best to spread the partitions and leadership fairly among the brokers
- Kafka is using Apache Zookeeper for all its coordination logic
- Kafka is using Zookeeper as a registry for broker as well as for monitoring and failure detection(ephemeral znodes, watchers, etc)

### Data Persistence in Kafka
- Kafka persists all its messages on disk 
- Even after messages are consumed by the consumers, the records still stay within Kafka for a configurable period of time
- Persistence allows new consumers to join and consumer older messages
- Consumers that failed in the process of reading/processing a message to retry
- Failed Brokers can recover very fast

### Articles
- https://kafka.apache.org/documentation/ 
- https://en.wikipedia.org/wiki/Apache_Kafka
- https://aws.amazon.com/what-is/apache-kafka/