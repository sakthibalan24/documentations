# Kafka Interview Preparation: Scenario-Based Questions

1.  A Kafka consumer processes a message and saves it to the database,
    but crashes before committing the offset. What happens?
2.  How do you prevent duplicate messages from creating duplicate
    records?
3.  What happens if a Kafka consumer goes down for 30 minutes?
4.  How do you handle a message that repeatedly fails processing?
5.  How do you guarantee message ordering in Kafka?
6.  What happens when the number of consumers is greater than the number
    of partitions?
7.  How do you handle a slow Kafka consumer when millions of messages
    are accumulating?
8.  Kafka is unavailable when your Spring Boot application saves a
    report. How do you prevent event loss?
9.  How do you ensure a critical Kafka message is not lost?
10. What is the difference between producer idempotence and consumer
    idempotence?
11. What happens if a consumer commits the offset before processing the
    message?
12. How do multiple microservices consume the same Kafka event
    independently?
13. How do you handle a consumer that takes 10 minutes to process a
    message?
14. What is a consumer rebalance, and how can it affect production?
15. How do you implement retry without blocking all other messages?
16. How do you process millions of Kafka events efficiently?
17. How do you handle schema changes when multiple services consume the
    same Kafka event?
18. How do you handle database and Kafka consistency when a consumer
    updates a database and publishes another event?
19. What is Kafka exactly-once processing? Does it guarantee that the
    database is updated only once?
20. Design a complete Kafka-based Report Management System.
