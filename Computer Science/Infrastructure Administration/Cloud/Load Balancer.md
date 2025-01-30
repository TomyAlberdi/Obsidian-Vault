Created: 2024-09-17 16:31
## Family Tree:
1. Computer
2. Infrastructure Administration
3. [[Cloud]]
-- -
A **load balancer** is a technology designed to distribute workloads across multiple servers or applications. The primary goal is to optimize overall infrastructure performance, enhance reliability, and improve capacity.
![[Computer Science/Infrastructure Administration/Cloud/attachments/image 8.png]]
**Elastic Load Balancing (ELB)**, for example, automatically distributes incoming application traffic across various targets, such as Amazon EC2 instances, containers, IP addresses, Lambda functions, and virtual appliances. Modern high-traffic websites must handle millions of simultaneous requests from users, delivering text, images, videos, or application data quickly and reliably. To scale efficiently and meet these high traffic demands, it is common practice to add more servers to the infrastructure.
A load balancer acts as a "traffic cop," routing user requests to any available servers that can fulfill them. This process maximizes both speed and server capacity utilization, ensuring that no single server is overwhelmed, which could degrade performance. If a server goes offline, the load balancer redirects traffic to the remaining active servers. When new servers are added, the load balancer automatically begins routing traffic to them.
## Key Functions
- **Efficient Distribution**: It distributes client requests or network traffic efficiently across multiple servers.
- **High Availability and Reliability**: Ensures that requests are only sent to servers that are online.
- **Scalability**: Provides the flexibility to add or remove servers as demand fluctuates.
## Benefits
- **Reduced Downtime**: Ensures traffic is redirected to available servers if one goes down.
- **Scalability**: Easily handles increased traffic by distributing requests across more servers.
- **Redundancy**: Adds fault tolerance by ensuring multiple servers can handle requests.
- **Flexibility**: Allows for dynamic scaling and adjustments to server infrastructure.
- **Efficiency**: Optimizes resource usage and improves overall system performance.