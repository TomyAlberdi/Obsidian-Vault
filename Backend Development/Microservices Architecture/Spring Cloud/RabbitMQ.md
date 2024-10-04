Created: 2024-10-04 20:10
## Family Tree:
1. Computer
2. Backend Development
3. Microservices Architecture
4. [[Spring Cloud]]
-- -
**RabbitMQ** is an open-source message broker developed in the Erlang programming language. Also known as a **Message Broker**, it acts as an intermediary between the producer (who sends messages) and the consumer (who receives them).
## Spring Cloud Stream
Modern systems aim for features like fault tolerance, scalability, event-driven architectures, and high availability. These systems are often distributed and rely heavily on **Message Brokers** to orchestrate and communicate between microservices. Message brokers provide enhanced scalability and allow for seamless communication between services.
Two popular message brokers are **Apache Kafka** and **RabbitMQ**, which are well-known for their robustness and simplicity. However, using these message brokers can involve a steep learning curve.
To simplify the usage of message brokers in modern architectures, **Pivotal** (the maintainer of Spring projects) created **Spring Cloud Stream**, which groups various messaging technologies to make them easier to implement.
### Messaging System:
In a messaging system, there are always:
- A **producer** who creates the messages, and
- A **consumer** who receives and processes them.
However, between the producer and consumer, there are two other key components:
1. **Exchange**
2. **Queue**
![[Backend Development/Microservices Architecture/Spring Cloud/attachments/image 5.png]]
#### Exchange:
Before the messages reach the queue, they pass through an exchange. The exchange is responsible for routing messages to the appropriate queue based on certain conditions. RabbitMQ offers four types of exchanges:
- **Direct**: 
  The message is routed directly to the queue based on a **routing key**. A **bind** links a specific queue to an exchange.
  ![[Backend Development/Microservices Architecture/Spring Cloud/attachments/image 6.png]]
- **Topic**: 
  A widely used exchange type, where messages are routed to queues based on specific rules and the routing key.
  ![[Backend Development/Microservices Architecture/Spring Cloud/attachments/image 7.png]]
- **Fanout**: 
  The message is sent to all queues associated with the exchange.
  ![[Backend Development/Microservices Architecture/Spring Cloud/attachments/image 8.png]]
- **Headers**: 
  Messages are routed to a queue based on header information, though this type is less common.
#### Queue:
This is where messages are stored until the consumer reads them. Once read, they are removed from the queue. Queues in RabbitMQ follow the **FIFO (First In, First Out)** principle. Key properties of queues include:
- **Durable**: 
  Persistent queues are saved to disk, ensuring that messages aren't lost if the broker restarts. Non-durable queues, however, are stored only in memory.
- **Auto-Delete**: 
  Automatically removes the queue when the consumer disconnects.
- **Expiry**: 
  Specifies the maximum idle time for the queue. If no messages are received within this time, the queue is deleted.
- **TTL (Time To Live)**: 
  The lifetime of a message in the queue. If a message isn’t consumed within this time, it is removed.
- **Queue Length Limit**: 
  Defines the maximum number of messages a queue can hold. Once the limit is reached, the queue can either:
    - **Drop head**: Removes the oldest message, or
    - **Reject publish**: Stops accepting new messages.
- **Max Length**: 
  The maximum number of messages or bytes allowed in a queue. If this limit is exceeded, an overflow occurs.
### RabbitMQ + Zipkin:
In another section, we discussed how services communicate asynchronously using **Message Brokers**. These messages typically have the following characteristics:
- **Asynchronous**.
- **High volume**.
- **Multiple emitters**.
Until now, we’ve considered these messages as business information (such as purchase orders, product data, etc.). Now, let's explore another common use case, focusing on a different type of information.
#### Logs and Latency Information:
Logs contain tracking data for a system. They can include errors (exceptions), execution info, debug messages, or latency data. **Latency information** refers to the input and output times of a service—essentially, how long it takes from receiving a request to generating a response. It makes sense to handle this data asynchronously by sending it to a **Message Broker** (like RabbitMQ), which centralizes all the information.
#### Distributed Tracing with Zipkin and RabbitMQ:
The `ZipkinDistributedTracingServer` connects to an in-memory database. All microservices will send trace information (errors, latency, debug data, etc.) via messages to the **RabbitMQ** server, where the `ZipkinDistributedTracingServer` consumes the messages.
![[Backend Development/Microservices Architecture/Spring Cloud/attachments/image 9.png]]
#### Dependencies:
To implement this setup, the following dependencies are required:
```xml
<dependency>
  <groupId>org.springframework.cloud</groupId>
  <artifactId>spring-cloud-starter-zipkin</artifactId>
</dependency>
<dependency>
  <groupId>org.springframework.cloud</groupId>
  <artifactId>spring-cloud-starter-sleuth</artifactId>
</dependency>
<dependency>
  <groupId>org.springframework.cloud</groupId>
  <artifactId>spring-cloud-sleuth-zipkin</artifactId>
</dependency>
<dependency>
  <groupId>org.springframework.amqp</groupId>
  <artifactId>spring-rabbit</artifactId>
</dependency>
```
#### Configuration:
Here’s how the **Spring configuration** looks to set up RabbitMQ and Zipkin:
```yml
spring:
  sleuth:
    sampler:
      probability: 1.0
  rabbitmq:
    addresses: localhost:5672
    virtual-host: app_vhost
    username: username
    password: password
  zipkin:
    baseUrl: http://localhost:9411/
    enabled: true
    sender:
      type: rabbit
    enabled: true
```
#### Explanation:
- **Zipkin** and **Sleuth** are integrated to capture trace information.
- **RabbitMQ** is configured to act as the message broker where trace data is sent.
- The **sampler** ensures that 100% of requests are traced (controlled via `probability`).
- The **Zipkin sender** uses RabbitMQ to deliver trace data asynchronously.
By combining **RabbitMQ** for message brokering and **Zipkin** for distributed tracing, we can effectively monitor the communication between microservices, identify bottlenecks, and troubleshoot performance issues.