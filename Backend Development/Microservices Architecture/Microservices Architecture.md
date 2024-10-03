Created: 2024-10-03 15:12
## Family Tree:
1. Computer
2. [[Backend Development]]
-- -
## Monolithic Architecture vs Microservices
Let's analyze monolithic architecture.
### Monolithic Architecture:
Think about the evolution of computers. At first, there was no connection between them (i.e., no Internet), and these computers were not personal but large computing centers. Clearly, this reality made early programs and subsequent ones self-sufficient, or in other words, systems composed of several interrelated modules within the same computer.
Later, both hardware and software evolved to the point where personal computers and network interconnectivity between them began to develop. This allowed resources to no longer be confined to a single computer, and the first web pages for various businesses, such as home banking and e-commerce, appeared. Let's look at an example of the latter.
If we think of a typical e-commerce platform, we can infer different modules outlined in the following diagram:
![[Backend Development/Microservices Architecture/attachments/image.png]]As we can observe, we will have different actions, such as searching for and adding a product, user login, user registration, product shipping logistics, alerts for important events, billing through various payment methods, and more.
We can also see that absolutely all functionality is integrated into a single software unit, using a single data persistence resource within a database. This means that, for example, the business logic for products and billing will be together, with coupling and cohesion depending on the logic defined by the developer.
#### Advantages:
- **What happens if there’s an error?** 
  All systems experience errors in a production environment. These can be either technical errors due to dependency failures like a database (DB) or functional failures like an incorrect email format. These errors are easily detectable in this type of architecture because the failure occurs in one location that encompasses all the solution’s modules or components.
- **Is the solution’s coupling a problem in terms of maintenance and production deployment?**
  While the coupling of the solution may be an issue for scalability, it is not for maintenance and production deployment. Maintaining a single centralized repository for the e-commerce business is less costly than maintaining multiple repositories, as long as the development team is small. A large team could create code conflicts due to concurrent changes. Similarly, deployment is much simpler when done as a whole rather than as the sum of parts.
#### Disadvantages:
- **What happens if I want to change the programming language to, for example, facilitate shipping logic?**
  Since the set of programming languages used to develop the monolithic application is unique (because all components work together within the same unit), we would need to change the language of the entire solution or externalize some components.
- **From the user's point of view, what would happen if our e-commerce experiences a sudden increase in traffic due to a special occasion like Christmas?**
  The system would become overloaded, unable to handle the added demand, leading to excessive response times across all functionalities. This translates into business problems, resulting in lost sales and profits for the organization.
- **What if our e-commerce begins to succeed and the demand for new functionality in existing modules grows significantly?**
  To meet user needs and avoid falling behind competitors, we would need to rapidly grow the team to reduce time to market (TTM) for delivering new features. As the team grows and everyone starts working on the same repository (since it’s a single integrated system), we’ll encounter code conflicts, failed unit tests due to module dependencies, and so on. This shows that this solution is not viable for systems with constant updates and new features.
### Microservices Architecture:
This architecture is the antithesis of monolithic architecture, as it does not couple functionalities as a whole. Instead, it creates small components with a single, well-defined functionality. These components have autonomy in terms of computational resources and dependencies like databases (DBs), allowing them to evolve independently over time.
A microservice is not necessarily a REST or SOAP service; rather, it handles a specific service—whether using these protocols or another method, such as batch processing, responding to an event triggered by messaging queues, processing a file via FTP, etc.
A typical e-commerce platform based on a microservices architecture would look like this:
![[Backend Development/Microservices Architecture/attachments/image 1.png]]
The **API Gateway** is a key component of this architecture. It serves as the entry point to the microservices ecosystem, where access rules for security can be imposed, usage quotas for microservices (how many requests can be made), operating hours, and network consumption limits for consumers can be set.
Visually, we can see that the large e-commerce software unit is now distributed across several microservices that, together, deliver the full functionality of the system. While they interact with each other to achieve a larger goal, each knows exactly what to do (hence, they are highly cohesive), achieving independence from other microservices by using its own information repository.
#### Advantages:
- **What happens if application consumption grows during Christmas, searches increase due to promotions, and the site starts to saturate?**
  In this architecture, we would only need to increase the number of instances of the product microservice, not the entire solution. This way, we can address the issue without wasting resources, which can later be reduced after the holiday season. This is possible thanks to the solution’s decoupling and infrastructure independence, a concept known as scalability.
- **What about TTM (Time to Market)?**
  TTM is enhanced and optimized in this type of architecture because a large development team can evolve each microservice independently with its own repository. For instance, we can optimally respond to business requirements for new shipping features without affecting the entire system.
- **What if I want to change the programming language?**
  As this is a distributed architecture with completely independent components, we can be polyglot with respect to programming languages. This means we can have microservices developed in Java, others in .NET, Node.js, etc. Depending on the functionality required, the most appropriate language can be chosen.
- **What is the benefit of having a large system as the sum of its parts?**
  We can say that those parts, which have a single purpose, are entirely reusable within the organization’s ecosystem.
#### Disadvantages:
- **What happens if there’s a failure?**
  Failures in this type of architecture are more complex to detect and fix. Since a microservice calls another to achieve a higher-level objective in a standard system, each call could potentially fail, and we need to manage these failures to maintain system integrity and ensure proper failover response.
- **Why is debugging and error discovery more complex?**
  Each microservice has its own log and execution context, so tracing the invocations between microservices is essential to identify the call chain of a user request and determine where to apply the fix.
- **Why can performance be impacted?**
  Each microservice has network latency when invoked. The response time is the sum of the chain of invoked microservices, so we must be cautious with resource usage, implemented algorithms, and response sizes to ensure optimal response times.