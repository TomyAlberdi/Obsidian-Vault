Created: 2024-10-03 16:07
## Family Tree:
1. Computer
2. Backend Development
3. Microservices Architecture
4. [[Computer Science/Backend Development/Microservices Architecture/Design Patterns/Design Patterns|Design Patterns]]
-- -
As developers, we are accustomed to implementing synchronous communication using I/O blocking (input/output blocking), such as with a RESTful JSON API over HTTP. In this scenario, a server receiving a request and preparing to send a response allocates a thread (within the operating system) for the duration of the request. If the number of simultaneous requests increases, the server could run out of available threads. This can lead to issues ranging from longer response times to server failures. In a microservices architecture, this problem is often exacerbated, as a series of cooperative microservices are usually involved in handling a request. The more microservices participating in a request, the faster the available threads are exhausted.
To address this issue, the **Non-Blocking Asynchronous Pattern** advocates using **non-blocking asynchronous calls** whenever possible. This includes common calls to slow resources over the network, database calls, request handling, and, in general, the entire call flow. By doing so, we need to use **reactive programming** to enable optimal and correct asynchronous communication between the REST APIs of the different microservices we create.
**Reactive systems** are more flexible, loosely coupled, and scalable. This makes them easier to develop and adapt to changes. They are significantly more resilient to failures, and when a failure occurs, they handle it pragmatically, preventing it from becoming a disaster.
## Example
Let's say we have an e-commerce platform with a checkout process for an order that involves checking offers, stock, and shipping. Each step takes 1 second (with an idle server), and the server has the capacity to maintain 10,000 open sessions simultaneously.
If our operation is **blocking synchronous**, the user will send their request, and after 3 seconds, all steps will be executed. During those 3 seconds, everything will be checked, but what happens if 10,000 orders come in at the same time? The first will execute correctly, the second will take a bit longer because it has to wait for the first, and by the time we reach 5,000 orders, the system degrades, and server errors begin to appear as it becomes overloaded.
Now, suppose our operation is **asynchronous**. The server receives the user's checkout request and sends the event to a **message queue** for the offers, stock, and shipping services to process the orders. The user receives the message "your order is being processed" in a fraction of a second, and the server is freed up. So, if we have 10,000 orders and another 10,000 come in the next second, the system doesn't degrade. Perhaps some "in-process" orders won't be fulfilled due to out-of-stock issues, but in practice, this approach is much better for several reasons:
- The server is not blocked, and we can continue receiving orders.
- The window for an outdated stock check is very small.
- Suppliers have a margin for stock safety.
- We can parallelize processes.