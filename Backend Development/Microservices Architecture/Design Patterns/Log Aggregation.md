Created: 2024-10-03 15:41
## Family Tree:
1. Computer
2. Backend Development
3. Microservices Architecture
4. [[Backend Development/Microservices Architecture/Design Patterns/Design Patterns|Design Patterns]]
-- -
When we talk about distributed architecture, one of the most frequent problems is obtaining **traceability** of service execution, since in this type of architecture, the execution of a service passes through multiple services. This makes it difficult to understand what is happening and to maintain a detailed log of events. Specifically, in architectures like microservices, it is common to have multiple instances of the same component, which makes retrieving the execution trace even more tedious.
To solve this problem, we have the **Log Aggregation** pattern. This pattern, using an external component, allows us to consolidate all logs into a single data source that we can consult later, without needing physical access to the servers and without concern for how many instances of each component are running. This way, by using this pattern, we can identify errors more efficiently, providing better service to our customers.