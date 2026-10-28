# Kafka Interview Preparation: Scenario-Based Questions

## Section 1: Message Delivery Semantics, Offsets, and Idempotence

1.  A Kafka consumer processes a message and saves it to the database,
    but crashes before committing the offset. What happens?
2.  How do you prevent duplicate messages from creating duplicate
    records?
3.  What is the difference between producer idempotence (`enable.idempotence=true`)
    and consumer idempotence?
4.  What happens if a consumer commits the offset before processing the
    message?
5.  What is Kafka exactly-once processing (EOS)? Does it guarantee that
    an external database is updated only once?
6.  How does `auto.offset.reset` behave when set to `earliest`, `latest`, or `none`,
    especially when a new consumer group starts or committed offsets expire?
7.  If you process Kafka messages asynchronously in a multi-threaded worker pool
    inside a single consumer, why can committing offsets lead to silent data loss,
    and how do you resolve it?
8.  How does Kafka's Transactional Producer (`transactional.id`) work across
    multiple topics and partitions in a consume-process-produce loop?

## Section 2: Consumer Architecture, Scaling, and Rebalancing

1.  What happens if a Kafka consumer goes down for 30 minutes?
2.  What happens when the number of consumers in a consumer group is greater
    than the number of partitions?
3.  How do you handle a slow Kafka consumer when millions of messages
    are accumulating?
4.  How do multiple microservices consume the same Kafka event
    independently?
5.  How do you handle a consumer that takes 10 minutes to process a
    message without triggering an unwanted rebalance?
6.  What is a consumer rebalance, and how can it affect production?
7.  What is the difference between Eager Rebalancing and Cooperative Sticky
    Rebalancing (`CooperativeStickyAssignor`), and how does the latter prevent
    "stop-the-world" consumer pauses?
8.  Explain the relationship and difference between `heartbeat.interval.ms`,
    `session.timeout.ms`, and `max.poll.interval.ms`.
9.  How do you pause and resume message consumption (`consumer.pause()` /
    `consumer.resume()`) to implement consumer-side backpressure?
10. How do you measure and alert on Kafka Consumer Lag using tools like
    Burrow, Prometheus JMX Exporter, or Kafka Lag Exporter?

## Section 3: Partitioning, Keys, and Message Ordering

1.  How do you guarantee message ordering in Kafka?
2.  What happens if a partition key is not specified when publishing a record
    (Murmur2 hash vs Sticky Partitioner in newer Kafka versions)?
3.  A specific customer generates 80% of all platform traffic, causing one
    partition to lag severely while others remain idle (Hot Partition / Key Skew).
    How do you resolve this?
4.  What happens to existing keyed messages when you increase the partition
    count of an active topic from 10 to 20?
5.  How does log compaction (`cleanup.policy=compact`) work, and what is the role
    of "tombstone" records (`null` payload) in deleting keys?
6.  How do you achieve per-entity (e.g., per-tenant or per-user) strict ordering
    while processing events concurrently across worker threads?

## Section 4: Broker Reliability, Replication, and Fault Tolerance

1.  Kafka is unavailable when your Spring Boot application saves an entity.
    How do you prevent event loss?
2.  How do you ensure a critical Kafka message is never lost across producers,
    brokers, and consumers?
3.  Explain the interplay between `acks=all`, `min.insync.replicas=2`, and
    topic `replication.factor=3`. What happens if two brokers crash?
4.  What are Under-Replicated Partitions (URP) and Offline Partitions, and
    what steps do you take to troubleshoot them?
5.  What is an "unclean leader election" (`unclean.leader.election.enable`),
    and what are the trade-offs between availability and data consistency?
6.  What is KRaft (Kafka Raft metadata mode), and how does it replace Apache
    ZooKeeper for metadata management and quorum elections?
7.  How do you implement Cross-Cluster Disaster Recovery and replication
    (Active-Passive vs Active-Active) using MirrorMaker 2.0, and how are
    consumer offsets translated across clusters?

## Section 5: Error Handling, Retries, and Dead Letter Queues

1.  How do you handle a message that repeatedly fails processing ("poison pill")?
2.  How do you implement non-blocking retries without blocking the consumption
    of subsequent messages in the partition?
3.  Design a complete Dead Letter Topic (DLT) architecture with exponential
    backoff, retry topics (e.g., `orders.retry-1m`, `orders.retry-5m`), and
    max-retry termination.
4.  Once the root-cause bug in a downstream service is fixed, how do you replay
    or redrive millions of failed messages stored in the Dead Letter Topic
    back into the primary processing pipeline?
5.  How do you prevent a poison pill from poisoning the Dead Letter Queue itself
    (e.g., deserialization failure before headers can be inspected)?

## Section 6: High Throughput, Performance Tuning, and Optimization

1.  How do you process millions of Kafka events efficiently?
2.  How do you optimize producer throughput using `batch.size`, `linger.ms`,
    and compression algorithms (`lz4`, `snappy`, `zstd`, `gzip`)?
3.  What happens when the producer memory buffer (`buffer.memory`) gets full,
    and how does `max.block.ms` impact the application thread?
4.  How does Kafka achieve high disk I/O performance despite writing to disk
    (sequential disk writes, OS page cache, and zero-copy `sendfile` system call)?
5.  A producer needs to send a 20 MB PDF/image payload, but Kafka default message
    limit is 1 MB. What are the pros and cons of increasing `message.max.bytes`
    versus implementing the Claim Check Pattern (S3/Blob storage)?
6.  How do you tune consumer fetch parameters (`fetch.min.bytes`,
    `fetch.max.wait.ms`, `max.partition.fetch.bytes`) for throughput vs latency?

## Section 7: Schema Governance and Evolution

1.  How do you handle schema changes when multiple microservices consume the
    same Kafka event?
2.  How does Confluent Schema Registry work with Avro/Protobuf/JSON Schema,
    and how is schema ID embedded into Kafka message bytes?
3.  Explain schema compatibility modes: `BACKWARD`, `FORWARD`, `FULL`, and `NONE`.
    Which mode allows deploying consumers before producers vs producers before consumers?
4.  How do you prevent breaking schema changes in a CI/CD pipeline before code
    is deployed to production?

## Section 8: Distributed Consistency and Dual-Write Patterns

1.  How do you handle database and Kafka consistency when a consumer updates
    a database and publishes another event?
2.  Explain the Transactional Outbox Pattern and how Change Data Capture (CDC)
    using Debezium and Kafka Connect eliminates the dual-write problem.
3.  What is the "Listen-to-Yourself" pattern, and when is it preferable to the
    Outbox pattern?
4.  How do you maintain distributed consistency across microservices using the
    Saga Pattern (Orchestration vs Choreography) with Kafka as the event backbone?

## Section 9: Security, Multi-Tenancy, and Governance

1.  How do you secure Kafka end-to-end using TLS encryption in transit and
    SASL authentication (SCRAM-SHA-512 / mTLS / Kerberos)?
2.  How do you define and enforce fine-grained topic permissions using Kafka
    Access Control Lists (ACLs)?
3.  One rogue client application is flooding the Kafka cluster with requests,
    affecting other critical services. How do you use Kafka Client Quotas
    (produce, fetch, and request quotas) to enforce rate limits?
4.  How do you comply with GDPR "Right to be Forgotten" requirements when Kafka
    logs are immutable by design?

## Section 10: Kafka Streams and Stateful Processing

1.  What is the difference between a stateless Kafka consumer and a stateful
    Kafka Streams application (KStream, KTable, GlobalKTable)?
2.  How does Kafka Streams use local RocksDB state stores and internal changelog
    topics for fault-tolerant state recovery?
3.  What happens during a Kafka Streams rebalance, and how do standby replicas
    (`num.standby.replicas`) minimize recovery time?
4.  How do you handle out-of-order and late-arriving events in windowed
    stream joins and aggregations?

## Section 11: Real-World Architecture & System Design Scenarios

1.  Design a complete Kafka-based Report Management System.
2.  Design a real-time Fraud Detection System processing 100,000 transactions/sec
    with low latency anomaly alerting.
3.  Design an E-Commerce Flash Sale / Inventory Reservation Pipeline preventing
    overselling under sudden bursts of 500,000 concurrent requests.
4.  Design an Event-Sourced Banking Account Balance and Audit Ledger using Kafka
    as the append-only source of truth.
