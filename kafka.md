## What is Apache Kafka ?

Apache Kafka is an open-source distributed event streaming platform. It is designed to handle large-scale, high-throughput, and fault-tolerant real-time data streaming. Kafka is built on the publish-subscribe messaging model and provides a distributed commit log architecture.

Key concepts in Apache Kafka:

1. Topics: Kafka organizes data streams into topics, which can be thought of as categorized channels for publishing and subscribing to events or records. Topics are divided into partitions to enable parallel processing.

2. Producers: Producers are responsible for publishing data or messages to Kafka topics. They write messages to the end of the topic's log.

3. Consumers: Consumers read and process data from Kafka topics. They subscribe to one or more topics and read messages in the order they were written.

4. Partitions: Topics in Kafka are divided into partitions, which are ordered, immutable sequences of records. Each partition can be replicated across multiple Kafka brokers to provide fault-tolerance and scalability.

5. Brokers: Kafka brokers are the individual instances or servers that form a Kafka cluster. They are responsible for maintaining and managing the topic partitions, handling producer and consumer requests, and replicating data across the cluster.

6. Consumer Groups: Consumers can be organized into consumer groups. Each consumer within a group reads from a subset of partitions within a topic, enabling parallel processing and load balancing.

7. Streams: Kafka Streams is a client library that allows for building real-time stream processing applications. It provides an API for processing and analyzing data streams from Kafka topics.

Apache Kafka offers several key features that make it popular for real-time data streaming:

- High-throughput and Scalability: Kafka is designed to handle high message throughput and can scale horizontally by adding more brokers and partitions.

- Fault-tolerance and Replication: Kafka replicates topic partitions across multiple brokers to ensure data durability and availability even in the event of broker failures.

- Durability: Kafka provides persistent storage of messages for a configurable amount of time, allowing messages to be replayed or consumed by new consumers.

- Real-time Stream Processing: With Kafka Streams, applications can process and analyze data streams in real-time, enabling continuous data processing and analytics.

- Integration Ecosystem: Kafka has a rich ecosystem of connectors and integrations, making it easy to connect with various systems and data sources.

Apache Kafka has become widely adopted in a range of industries, including finance, e-commerce, social media, and IoT, where real-time data processing, messaging, and event-driven architectures are essential.

## How kafka broker work ?

Apache Kafka is an open-source distributed event streaming platform. It is designed to handle large-scale, high-throughput, and fault-tolerant real-time data streaming. Kafka is built on the publish-subscribe messaging model and provides a distributed commit log architecture.

Key concepts in Apache Kafka:

1. Topics: Kafka organizes data streams into topics, which can be thought of as categorized channels for publishing and subscribing to events or records. Topics are divided into partitions to enable parallel processing.

2. Producers: Producers are responsible for publishing data or messages to Kafka topics. They write messages to the end of the topic's log.

3. Consumers: Consumers read and process data from Kafka topics. They subscribe to one or more topics and read messages in the order they were written.

4. Partitions: Topics in Kafka are divided into partitions, which are ordered, immutable sequences of records. Each partition can be replicated across multiple Kafka brokers to provide fault-tolerance and scalability.

5. Brokers: Kafka brokers are the individual instances or servers that form a Kafka cluster. They are responsible for maintaining and managing the topic partitions, handling producer and consumer requests, and replicating data across the cluster.

6. Consumer Groups: Consumers can be organized into consumer groups. Each consumer within a group reads from a subset of partitions within a topic, enabling parallel processing and load balancing.

7. Streams: Kafka Streams is a client library that allows for building real-time stream processing applications. It provides an API for processing and analyzing data streams from Kafka topics.

Apache Kafka offers several key features that make it popular for real-time data streaming:

- High-throughput and Scalability: Kafka is designed to handle high message throughput and can scale horizontally by adding more brokers and partitions.

- Fault-tolerance and Replication: Kafka replicates topic partitions across multiple brokers to ensure data durability and availability even in the event of broker failures.

- Durability: Kafka provides persistent storage of messages for a configurable amount of time, allowing messages to be replayed or consumed by new consumers.

- Real-time Stream Processing: With Kafka Streams, applications can process and analyze data streams in real-time, enabling continuous data processing and analytics.

- Integration Ecosystem: Kafka has a rich ecosystem of connectors and integrations, making it easy to connect with various systems and data sources.

Apache Kafka has become widely adopted in a range of industries, including finance, e-commerce, social media, and IoT, where real-time data processing, messaging, and event-driven architectures are essential.

## Leader and follower concept in Kafka

In Apache Kafka, the leader and follower concepts are related to the replication mechanism used to ensure fault-tolerance and data availability. They are associated with the partitioning of topics and are responsible for handling read and write operations for a given partition.

When a topic is created in Kafka, it is divided into multiple partitions, and each partition is replicated across multiple brokers in a Kafka cluster. Within each partition, one broker is designated as the leader, and the remaining brokers hold replicas as followers. The leader and follower roles can change dynamically based on the state of the cluster.

Here's how the leader and follower concept works in Kafka:

1. Leader: The leader replica is responsible for handling all read and write operations for a partition. Producers send messages to the leader, which appends them to the end of the partition's log. Consumers read messages from the leader, and it serves as the primary point of contact for all client interactions related to the partition.

2. Follower: Followers replicate the data from the leader and keep their copies of the partition up to date. They act as backup replicas and can take over as the leader if the current leader fails. Followers continuously fetch data from the leader and maintain a copy of the partition's log. However, they do not serve read or write requests directly from clients.

3. Replication and Data Consistency: Kafka ensures data consistency and fault-tolerance through replication. Each partition has a configurable replication factor that determines the number of replicas it should have. The leader writes messages to its local log and then replicates them to the followers. Followers maintain a replica of the leader's log by continuously fetching the latest data. This replication process ensures that followers remain in sync with the leader, allowing for failover and data durability.

4. Leader Election: If the leader fails, one of the followers is elected as the new leader to ensure continuity of operations. The leader election process takes place automatically and is based on a combination of factors such as availability, health, and synchronization lag of the replicas. Once a new leader is elected, it starts handling read and write operations for the partition.

Benefits of the leader and follower concept:

- High Availability: The leader and follower replication mechanism ensures that even if the leader fails, one of the followers can take over as the new leader, allowing for continuous availability of the partition's data.

- Scalability: Kafka allows for horizontal scalability by distributing partitions across multiple brokers. Each broker can serve as a leader or follower for different partitions, enabling parallel processing and high throughput.

- Data Durability: Replication of partitions across multiple brokers ensures data durability. Even if a broker fails, the replicated data on other brokers can be used to recover and continue processing without data loss.

The leader and follower concept in Kafka is fundamental to providing fault-tolerance, data availability, and scalability in distributed event streaming scenarios. It allows for reliable and efficient handling of read and write operations on Kafka topics.

## Kafka acknowledgment

In Apache Kafka, acknowledgment (also known as ack) refers to the mechanism by which producers and brokers confirm the successful delivery and processing of messages. Kafka provides different levels of acknowledgment to allow producers to control the trade-off between message durability and write throughput. The acknowledgment mechanism ensures that messages are reliably processed and replicated within the Kafka cluster.

Kafka offers three levels of acknowledgment:

1. Acknowledgment Level 0 (acks=0): In this mode, the producer does not wait for any acknowledgment from the broker after sending a message. The producer simply writes the message to the internal buffer and continues without any assurance of successful delivery. This mode provides the highest write throughput but offers no guarantees regarding message durability or replication.

2. Acknowledgment Level 1 (acks=1): This mode requires the broker leader to acknowledge the receipt of the message. The producer waits for an acknowledgment from the leader before considering the message as successfully sent. Once the leader acknowledges the message, the producer can continue producing more messages. This mode provides a balance between write throughput and reliability.

3. Acknowledgment Level -1 (acks=all): This mode ensures that the message is replicated to all in-sync replicas (ISRs) of the partition before the producer receives an acknowledgment. ISRs are a subset of replicas that are fully caught up with the leader. This level of acknowledgment provides the strongest durability and replication guarantees but has the slowest write throughput due to the additional replication overhead.

When a producer receives an acknowledgment, it knows that the message has been successfully written to the Kafka broker and replicated according to the specified acknowledgment level. If an acknowledgment is not received within a configured timeout period, the producer can retry sending the message to ensure its successful delivery.

The choice of acknowledgment level depends on the application's requirements for durability, reliability, and write throughput. For scenarios where low-latency and high throughput are crucial, acks=0 may be suitable. For use cases where durability and reliability are more important, acks=1 or acks=all can be used.

It's important to note that acknowledgments from brokers confirm the successful delivery of messages to the Kafka cluster; they do not indicate whether consumers have processed the messages. To ensure end-to-end delivery and processing guarantees, consumers need to implement their own acknowledgment mechanism, such as committing offsets after processing messages.

By providing different acknowledgment levels, Kafka allows producers to make an informed decision about trading off write throughput with durability and replication guarantees, enabling flexible and reliable message handling in distributed systems.

## Common Kafka config

1. `bootstrap.servers`: This configuration specifies the list of bootstrap servers that the Kafka client connects to initially to discover the full set of brokers in the Kafka cluster. It should be set to a comma-separated list of `<host>:<port>` pairs.

2. `group.id`: This configuration is used to specify the consumer group ID. Consumers that belong to the same group share the workload of consuming partitions from topics. Kafka uses group IDs to track the offset commit position for each consumer group.

3. `acks`: This configuration is specific to the producer and determines the number of acknowledgments the producer requires from brokers for successful message writes. The possible values are `0` (no acknowledgment), `1` (acknowledgment from the leader), and `all` (acknowledgment from all in-sync replicas).

4. `auto.offset.reset`: This configuration is used by consumers when they start consuming a topic or partition that doesn't have a committed offset or when the committed offset is no longer valid. It specifies the strategy for resetting the offset. Possible values include `earliest` (start from the earliest available offset) and `latest` (start from the latest offset).

5. `enable.auto.commit`: This configuration determines whether the consumer commits offsets automatically. If set to `true`, the consumer periodically commits the offsets it has processed. If set to `false`, the consumer requires manual offset management.

6. `max.poll.records`: This configuration controls the maximum number of records that a consumer can fetch in a single poll request to the broker. It helps control the batch size of records returned to the consumer.

7. `max.partition.fetch.bytes`: This configuration specifies the maximum amount of data (in bytes) the consumer can fetch from a single partition in a single request. It affects the maximum size of the records returned to the consumer.

8. `message.max.bytes`: This configuration sets the maximum size of a Kafka message (including key and value) that the broker will accept for writing to a topic. It helps prevent oversized messages from being produced.

9. `num.partitions`: This configuration is used when creating a new topic. It specifies the number of partitions for the topic. Increasing the number of partitions allows for parallelism in message processing.

10. `replication.factor`: This configuration is also used when creating a new topic. It defines the number of replicas that should be maintained for each partition. Replication provides fault-tolerance and data availability.

11. `compression.type`: This configuration specifies the compression type for message payloads that are produced by the producer. Supported compression types include `none`, `gzip`, `snappy`, `lz4`, and `zstd`. Compression can help reduce network bandwidth and storage requirements.

12. `fetch.min.bytes`: This configuration defines the minimum amount of data (in bytes) that the consumer requests from a broker in a single fetch request. If the broker has fewer bytes than this value, it waits until more data is available or the fetch.max.wait.ms time elapses.

13. `fetch.max.bytes`: This configuration sets the maximum amount of data (in bytes) that the consumer can fetch from a broker in a single fetch request. It limits the size of the response returned to the consumer.

14. `fetch.max.wait.ms`: This configuration specifies the maximum amount of time the consumer waits for new data to arrive in a fetch request. If no new data is available within this time, the broker returns a response to the consumer with whatever data it has.

15. `linger.ms`: This configuration controls the amount of time the producer waits before sending a batch of messages. It allows the producer to accumulate more messages in a single batch, improving throughput and reducing the overhead of sending frequent smaller batches.

16. `max.in.flight.requests.per.connection`: This configuration determines the maximum number of unacknowledged requests that can be in-flight to a broker. It helps control the degree of parallelism for the producer.

17. `max.poll.interval.ms`: This configuration sets the maximum time (in milliseconds) that the consumer can be idle during a poll before it is considered inactive and its partitions are reassigned to another consumer in the same group.

18. `metadata.max.age.ms`: This configuration specifies the maximum time (in milliseconds) that the client will cache metadata about the Kafka cluster. After this time elapses, the client will refresh the metadata for topics and partitions.

19. `request.timeout.ms`: This configuration sets the maximum time (in milliseconds) that a client will wait for a response from the Kafka broker for various requests, such as produce, fetch, or metadata requests.

20. `socket.receive.buffer.bytes` and `socket.send.buffer.bytes`: These configurations control the size of the TCP socket receive and send buffers, respectively. Adjusting these values can help optimize network I/O performance.
