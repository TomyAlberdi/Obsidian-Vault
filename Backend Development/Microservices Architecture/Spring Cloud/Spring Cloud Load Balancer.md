Created: 2024-10-04 15:45
## Family Tree:
1. Computer
2. Backend Development
3. Microservices Architecture
4. [[Spring Cloud]]
-- -
## Load Balancing
**Load Balancing** refers to the efficient distribution of incoming network traffic across a group of backend servers. In other words, a load balancer routes client requests to servers capable of handling them, maximizing processing capacity and speed while ensuring no server is overwhelmed, which could reduce performance.
If a server fails, the load balancer redirects traffic to the available servers. Likewise, when a new server is added, the load balancer begins directing requests to it.
There are two main types of load balancing:
### Client-Side Load Balancing:
In this model, the client is responsible for distributing the load by sending requests to different servers. The client can use a service registry, like **Eureka**, to obtain a list of available instances and their locations.
**Advantages**:
- **No need for an additional component**: You don't have to worry about the high availability of a load balancer.
- **Reduced latency and infrastructure costs**: Since the request is sent directly to the server without an intermediary load balancer, this can lower latency and reduce the costs of infrastructure and maintenance.
### Server-Side Load Balancing:
In this model, all instances are registered with the load balancer. The client sends a request to the load balancer, and the balancer redirects the request to one of the available instances.
**Features**:
- **Load balancing algorithms**: The load balancer offers various algorithms to select from based on the requirements.
The most common algorithm is **Round-Robin**, where requests are distributed to instances in a fixed order, and once all instances have been used, the process repeats from the first instance. However, round-robin can have issues when you need to maintain session consistency. For example, if a user’s session is handled by different servers on each request, it could lead to problems with data consistency.
In such cases, you can use **Affinity-based load balancing**, which directs all requests from a specific user to the same server, preserving session state.
## Spring Cloud Load Balancer
To configure **Spring Cloud Load Balancer**, follow these steps:
### Add the Dependency:
First, add the necessary dependency to your project's `pom.xml` file:
```xml
<dependency>
   <groupId>org.springframework.cloud</groupId>
   <artifactId>spring-cloud-starter-loadbalancer</artifactId>
</dependency>
```
### Enable Service Discovery with Eureka:
The load balancer will retrieve the running instances of each microservice from **Eureka**. To enable this, add the `@EnableDiscoveryClient` annotation in the main class of the microservice that will make the requests:
```java
@SpringBootApplication
@EnableFeignClients
@EnableDiscoveryClient
public class Application {
  public static void main(String[] args) {
    SpringApplication.run(Application.class, args);
  }
}
```
### Using Spring Cloud Load Balancer with Feign:
Once the necessary dependencies are added, **Feign** will automatically use the **Round-Robin** method for load balancing by default. No additional annotations or configurations are required for this basic behavior. However, if you want to customize the load balancer, such as changing the algorithm or adding a new one, follow these steps:
#### Example of Custom Load Balancer Configuration (Random Selection Algorithm):
```java
public class CustomLoadBalancerConfiguration {
    @Bean
    ReactorLoadBalancer<ServiceInstance> randomLoadBalancer(Environment environment, LoadBalancerClientFactory loadBalancerClientFactory) {
       String name = environment.getProperty(LoadBalancerClientFactory.PROPERTY_NAME);
       return new RandomLoadBalancer(loadBalancerClientFactory.getLazyProvider(name, ServiceInstanceListSupplier.class), name);
    }
}
```
In this example, we're creating a method that will use a **random selection algorithm** for load balancing. By annotating this method with `@Bean`, it will be registered as a custom load balancer.
### Apply the custom Lead Balancer Configuration in Feign Client:
Once the custom load balancer configuration is defined, you need to apply it to the **Feign client**. Use the `@LoadBalancerClient` annotation in the interface where the Feign client was previously defined:
```java
@FeignClient(name = "product-service")
@LoadBalancerClient(name = "product-service", configuration = CustomLoadBalancerConfiguration.class)
public interface ProductClient {
    @RequestMapping(method = RequestMethod.GET, value = "/products")
    List<ProductDTO> getProducts();
}
```
Here, the `@LoadBalancerClient` annotation is used to specify the **custom load balancing configuration** (`CustomLoadBalancerConfiguration.class`) for the `product-service`. This configuration overrides the default Round-Robin algorithm with the **random selection** algorithm defined earlier.
## Load Balancing Algorithms Examples
Here’s a breakdown of the different **load balancing strategies** commonly used in distributed systems:
- **Round-robin**:
    - For each incoming request, a different instance of the service is chosen in a cyclic, repeating order.
    - This approach evenly distributes the requests across all available instances.
    - **Example**: If there are 3 instances (A, B, C), the first request goes to A, the second to B, the third to C, and then it repeats.

- **Least connections**:
    - The load balancer directs the request to the instance with the fewest concurrent connections.
    - **Use case**: This strategy is effective when there's a significant variation in processing time for different requests, ensuring that overloaded servers aren't burdened with additional requests.

- **Weighted metric**:
    - A weighted metric is used to decide which instance will receive the next request. Metrics such as CPU usage, memory consumption, or custom-defined weights can determine which instance is best suited to handle the request.
    - **Example**: If one instance has a higher CPU load, it will receive fewer requests compared to instances with lower CPU loads.

- **Random**:
    - In this strategy, an instance is randomly chosen to handle the request.
    - **Benefit**: This can provide a quick and simple solution but doesn't account for server load or other metrics.

- **Sticky Session** (Session affinity):
    - The load balancer assigns requests from a specific user to the same server (instance) using a cookie or session ID.
    - **Use case**: This is helpful for applications that rely on **session-based data**, ensuring that all of a user’s requests are handled by the same server to maintain session consistency (e.g., when managing user login sessions).