Created: 2024-10-03 15:35
## Family Tree:
1. Computer
2. Backend Development
3. Microservices Architecture
4. [[Backend Development/Microservices Architecture/Design Patterns/Design Patterns|Design Patterns]]
-- -
Normally, an application is deployed along with its configuration, which might include a set of environment variables and/or files containing configuration information. In a microservices-based architecture, where there are many instances of microservices deployed, the following questions arise:
- How can I get a complete overview of the configuration for all the running microservice instances?
- How do we update the configuration while ensuring that all affected microservice instances adopt the same configuration?
The **Configuration Server** pattern provides a solution by introducing a new component, the **Configuration Server**, where the configuration for all microservices is stored.
At the same time, this allows all information to be centralized in one place, even supporting different configurations based on the environment (development, testing, QA, production, etc.).