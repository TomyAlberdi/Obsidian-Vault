Created: 2024-10-03 17:15
## Family Tree:
1. Computer
2. Backend Development
3. Microservices Architecture
4. [[Spring Cloud]]
-- -
## Declarative Invocations
Declarative invocations are designed to simplify the integration between microservices by enabling developers to create HTTP clients declaratively. Instead of manually coding the logic for connecting and invoking an API, developers only need to declare the necessary interfaces and annotate the methods to be invoked.
**Feign** is a tool used for making declarative HTTP invocations, originally developed by Netflix. It has now been integrated into Spring Cloud and is known as **Spring Cloud OpenFeign**. Here are some of the key advantages:
- **Service Discovery**: Using Eureka, Feign can discover microservices by name rather than requiring a URL made up of an IP address and port.
- **Load Balancing**: Feign can integrate with a load balancer like **Spring Cloud LoadBalancer**.
## Spring Cloud OpenFeign Setup
### Add Dependency:
To use Feign in a Spring Boot project, you need to add the following dependency in your `pom.xml`:
```xml
<dependency>
   <groupId>org.springframework.cloud</groupId>
   <artifactId>spring-cloud-starter-openfeign</artifactId>
</dependency>
```
### Enable Feign:
Enable Feign in the main class of your Spring Boot application by adding the `@EnableFeignClients` annotation:
```java
@SpringBootApplication
@EnableFeignClients
public class Application {
  public static void main(String[] args) {
    SpringApplication.run(Application.class, args);
  }
}
```
## Make requests to another Microservice registered in Eureka
Let’s assume we have a **product-service** that exposes a REST API. One of its methods returns all products via a **GET** request at `http://localhost:8080/products`.
Since the microservice is registered in **Eureka**, we can access the same resource by replacing `localhost` and `8080` with the service name registered in Eureka. So the new URL would be: `http://product-service/products`.
With **Feign**, we use interfaces to create the clients and send the requests.
### Create a DTO:
Create a Data Transfer Object (DTO) to store the response:
```java
public class ProductDTO {
  private Integer id;
  private String title;
  private String color;
  // Getters and setters
}
```
### Create a Feign Interface:
Now create an interface where Feign is configured to send the request:
```java
@FeignClient(name = "product-service")
public interface ProductClient {
  @RequestMapping(method = RequestMethod.GET, value = "/products")
  List<ProductDTO> getProducts();
}
```
- The value passed to `@FeignClient(name = "product-service")` is the name of the microservice registered in Eureka. Feign will use this to look up the physical address of the service.
- `@RequestMapping` specifies the HTTP method and the URL path to invoke. Here, it's a **GET** request to `/products`.
- Feign automatically parses the JSON response into the specified `ProductDTO` class.}
## Make requests to external Microservices
Feign can also send requests to services that are external or not registered with Eureka. You just need to provide the URL explicitly. For example, let’s say we want to get the location of a visitor using their IP address via an external API. The API endpoint is `http://ipwhois.app/json/{IP}`.
### Configure Feign for an external Service:
Here’s how to set up the Feign client for this external API:
```java
@FeignClient(name = "ip-service", url = "http://ipwhois.app/json")
public interface IpClient {
  @RequestMapping(method = RequestMethod.GET, value = "/{ip}")
  JsonNode getLocationByIp(@PathVariable("ip") String ip);
}
```
- The `url` attribute in `@FeignClient` is used to specify the external URL.
- The `@RequestMapping` is used to map the HTTP request, where the IP address will be passed as a path variable.
### Inject the Feign Client into a Service:
To use the Feign client, inject it into a service like so:
```java
@Service
public class ProductService {
  @Autowired
  private ProductClient productFeignClient;

  public List<ProductDTO> fetchAllProducts() {
    return productFeignClient.getProducts();
  }
}
```
In this example, the `ProductClient` interface is injected into the `ProductService` class, allowing us to fetch all products by calling `fetchAllProducts()`.