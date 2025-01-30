Created: 2024-10-03 15:28
## Family Tree:
1. Computer
2. Backend Development
3. Microservices Architecture
4. [[Computer Science/Backend Development/Microservices Architecture/Design Patterns/Design Patterns|Design Patterns]]
-- -
One of the most common problems when working with services is the need to know exactly where each service is located. As companies grow, the number of services required to support operations increases as well. This makes it increasingly difficult to know the exact location of each service (IP, port).
## Service Registry
This pattern allows the creation of a centralized server where all services register when they start up. In this way, each service must send its IP address, the corresponding port to the server, and, finally, the service identifier (usually an alphanumeric name that helps identify it). This way, the central server or registry will know exactly where each available service is.
This pattern ensures that we know exactly which services are available and their access paths. It typically provides a graphical interface that allows us to see the entire universe of active services.
Another feature is that services that register must constantly send a signal to the registry, known as a _heartbeat_. This indicates that the services remain available over time. If the registry does not receive this signal, the microservice is automatically marked as out of service, and a notification can be sent to an administrator or DevOps team to manage the issue.
We can conclude that the **Service Registry** is an essential component in a microservices architecture because it allows services to register regardless of their physical location. This makes it easy to locate them and later use auto-discovery techniques to find and load balance them.
## Service Discovery
The Service Registry pattern is complementary to the Service Discovery pattern. But before delving deeper, it's essential to clarify that in cloud architectures, _elasticity_ refers to the cloud's ability to grow or shrink resources as demand increases or decreases. This allows resource provisioning or expanding the processing capacity of existing servers on-demand without human intervention.
Therefore, if the cloud is elastic, it doesn't make sense to have a fixed configuration file where the addresses of each service are stored because it would require someone to continuously update that file whenever an instance is added or removed.
This is where **Service Discovery** comes into play, tasked with determining all active instances of services via a central registry, which is the Service Registry we previously discussed.
Service Discovery is a component responsible for retrieving from the Service Registry all instances of available services and performing load balancing. However, there are two ways this discovery can occur: client-side and server-side.
- **Client-Side View**: The client queries the registry for available services and then performs the load balancing between available instances.
- **Server-Side View**: The server is responsible for service discovery, hiding this capability from the client. Therefore, the client communicates with a single address, which internally resolves service discovery and load balancing.
In conclusion, like the Service Registry, Service Discovery is one of the most important patterns when implementing microservices or cloud-native architectures. This is because it allows us to decouple from physical servers and scale rapidly simply by spinning up new instances.