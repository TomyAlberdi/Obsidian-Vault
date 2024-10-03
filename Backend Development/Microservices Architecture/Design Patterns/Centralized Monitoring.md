Created: 2024-10-03 16:04
## Family Tree:
1. Computer
2. Backend Development
3. Microservices Architecture
4. [[Backend Development/Microservices Architecture/Design Patterns/Design Patterns|Design Patterns]]
-- -
If the response times observed or hardware resource usage become unacceptably high, it can be very difficult to identify the cause of the problem. We need the ability to analyze the consumption of hardware resources by each microservice. To achieve this, we can introduce a new component: the **Monitor Service**, which is capable of collecting metrics on hardware resource usage for each microservice instance. This will allow us to:
- Collect metrics from all servers used by the system environment, including auto-scaling servers.
- Detect new microservice instances as they are launched on available servers and begin collecting metrics from them.
- Provide an API and graphical tools to query and analyze the collected metrics.
- Set up alerts that trigger when a specific metric exceeds a defined threshold value.