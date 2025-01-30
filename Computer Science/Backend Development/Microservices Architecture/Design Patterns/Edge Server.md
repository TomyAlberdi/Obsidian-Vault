Created: 2024-10-03 15:33
## Family Tree:
1. Computer
2. Backend Development
3. Microservices Architecture
4. [[Computer Science/Backend Development/Microservices Architecture/Design Patterns/Design Patterns|Design Patterns]]
-- -
In many cases, within a microservices architecture, it is necessary to expose certain microservices outside of our system while hiding others from external access. The microservices that are exposed to the outside must be protected from malicious client requests. This is where the **Edge Server** plays a key role, serving as the gateway through which all external requests pass.
Typically, a component like this behaves as a **reverse proxy** and can be integrated with **Service Discovery** to offer dynamic load balancing capabilities.
To protect against malicious requests, we can employ standard protocols and best practices—such as **OAuth**, **OIDC** (OpenID Connect), **JWT** (JSON Web Token), and **API Keys**—to ensure that requests come from trusted sources. Similarly, microservices that require this "invisibility layer" can be made visible only to those that need their service by properly configuring the access routes to them.