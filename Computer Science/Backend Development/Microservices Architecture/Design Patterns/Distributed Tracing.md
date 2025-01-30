Created: 2024-10-03 15:42
## Family Tree:
1. Computer
2. Backend Development
3. Microservices Architecture
4. [[Computer Science/Backend Development/Microservices Architecture/Design Patterns/Design Patterns|Design Patterns]]
-- -
One of the main challenges in a distributed architecture is **traceability** of process execution, because a single call can trigger multiple service calls. This means we often have to retrieve logs in parts—essentially extracting each log from every microservice and then combining them, which can be a daunting and complex task. For this reason, it’s important to implement a **distributed tracing system** that allows us to unify logs in a single point and group them by execution.
To analyze delays in a series of calls between cooperating microservices, we need to collect **timestamps** for when requests, responses, and messages enter and leave each microservice.
When one microservice communicates with another, it sends the **global transaction ID** and its own **transaction ID** in its request. If a microservice does not receive these IDs, it generates them. In the HTTP protocol, these IDs are sent and received through **headers**. These IDs allow us to correlate all the traces emitted by different microservices processes in the same application request. By performing a global search for the global ID, we can retrieve the full set of traces emitted by the microservices through which the request passed.
We must ensure that all related requests and messages are tagged with a common **correlation ID**, and that this correlation ID is part of all logging events. Based on a correlation ID, we can use the centralized logging service to find all related log events.