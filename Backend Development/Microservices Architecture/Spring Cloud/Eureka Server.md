Created: 2024-10-03 16:20
## Family Tree:
1. Computer
2. Backend Development
3. Microservices Architecture
4. [[Spring Cloud]]
-- -
The microservices architecture style is not just about building individual services, but about ensuring that interactions between services are reliable and fault-tolerant.
In such an architecture, each microservice resides at a dynamically assigned IP address and port. This dynamic nature makes it difficult for a client to request a microservice, such as one exposing a REST API over HTTP.
Consider the following diagram:
![[Backend Development/Microservices Architecture/Spring Cloud/attachments/image.png]]
We have a service with three instances, each located in a different location. How could the client know the address of each one? Furthermore, how could the client determine which instance has the least load to process the request?
To address this issue, we need to add a new component to our architecture that allows us to:
- **Automatically register microservices and their instances** as soon as they are running, and remove them from the registry when they stop running or responding.
- The client must be able to send requests to microservices **without knowing their exact location**.
- Requests to a microservice’s instances should be **load-balanced** to distribute the requests evenly.
In **Spring Cloud**, this component is **Eureka**, which we will examine in detail below.
## Eureka Server Architecture
Eureka can be divided into two main components:
- **Eureka Client**: Responsible for publishing the information of the microservice where it is located.
- **Eureka Server**: Responsible for collecting the information from all the clients.
![[Backend Development/Microservices Architecture/Spring Cloud/attachments/image 1.png]]
## Configuration
**Eureka implements client-side service discovery**, meaning that clients communicate with the discovery server (Eureka server) to get information about available microservice instances. Below, we will see how to configure **Eureka client** and **Eureka server**.
### Eureka Client Configuration:
To configure Eureka client in our project, we first need to add the following dependency:
```xml
<dependency>
   <groupId>org.springframework.cloud</groupId>
   <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
</dependency>
```
By simply adding this dependency, our application will automatically register itself with the Eureka server. We just need to specify where the Eureka server is running (by default, it will run on port 8761) in the `application.properties` file:
```properties
eureka.client.service-url.defaultZone=http://localhost:8761/eureka
```
A very important property to configure is `spring.application.name`. This property is used to give each microservice a hostname. Clients will use this name to form the URL when communicating with the service:
```properties
spring.application.name=my-service
```
To disable the Eureka client in our project, we can add:
```properties
eureka.client.enabled=false
```
### Eureka Server Configuration:
To configure the Eureka server, we first need to add the following dependencies:
```xml
<dependency>
  <groupId>org.springframework.cloud</groupId>  
  <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
</dependency>
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-web</artifactId>
</dependency>
<dependency>
  <groupId>org.springframework.boot</groupId>        
  <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```
Next, we add the `@EnableEurekaServer` annotation in the main class of our project:
```java
@SpringBootApplication
@EnableEurekaServer
public class Application {
  public static void main(String[] args) {
   new SpringApplicationBuilder(Application.class).web(true).run(args);
  }
}
```
In the `application.properties` file, Eureka server can act as both a client and a server simultaneously. To prevent it from registering itself as a client, we set the following properties to `false`:
```properties
eureka.client.register-with-eureka=false 
eureka.client.fetch-registry=false
```
We also configure the port:
```properties
server.port=8761
```
Now, we can run our project and access the main dashboard of Eureka at:[http://localhost:8761/eureka/](http://localhost:8761/eureka/). This is where we can monitor the registered microservices and their instances.
## Actuator (Heartbeat Monitoring)
In a microservices ecosystem with multiple instances, it's necessary to monitor these instances for errors, load balancing, or to analyze metrics to determine if more instances of a particular service are needed. Common issues can include application exceptions, timeouts, or instance errors. Application errors are exceptions programmed into the code, while instance errors might involve issues like running out of disk space or memory. Timeout errors occur when a response takes longer than a specified threshold.
Clearly, it's inefficient to monitor each endpoint and send "inert" data constantly. In practice, special endpoints are used to return critical information about the health and status of the instance and service.
**Spring Boot Actuator** is the solution offered by the Spring framework to handle this problem. It automatically generates the necessary endpoints for monitoring. These endpoints can be "probed" by load balancers or other applications to manage traffic, such as Eureka.
Spring Boot Actuator provides ready-to-use functionalities in a production environment to monitor your application, collect metrics, analyze traffic, and check the state of your database—without the need for manual implementation.
Actuators are primarily used to expose operational information about a running application (health, metrics, info, dump, environment, etc.) via a REST API.
### Common Actuator Endpoints:

| Endpoint           | Description                                                                                                         |
| ------------------ | ------------------------------------------------------------------------------------------------------------------- |
| `/health`          | Shows information about the health of the application. A simple "status" if unauthenticated, detailed if logged in. |
| `/info`            | Displays arbitrary information about the application.                                                               |
| `/metrics`         | Displays metrics information of the application.                                                                    |
| `/trace`           | Displays trace information (by default, the last HTTP requests).                                                    |
| `/serviceregistry` | Shows the registration status with Eureka Server.                                                                   |
By default, only the `/health` endpoint is enabled for consumption. To enable additional endpoints, configure the following property in the `application.properties` file:
```properties
management.endpoints.web.exposure.include=serviceregistry,health,info
```
In the example above, we enabled the `/serviceregistry`, `/health`, and `/info` endpoints. To enable all endpoints, you can use:
```properties
management.endpoints.web.exposure.include=*
```
For more information on all the available Actuator endpoints:  
[Spring Boot Actuator Documentation](https://docs.spring.io/spring-boot/docs/current/reference/html/actuator.html#actuator.endpoints.exposing)
### Eureka Integration:
Eureka Server uses the `/health` and `/info` endpoints to obtain information about the microservices. By default, if you make an HTTP GET request to the `/health` endpoint, it responds with:
```json
{
  "status": "UP"
}
```
For the `/info` endpoint, you can customize the response by configuring certain properties. For example:
```properties
info.app.name=my-service
info.app.description=Testing Eureka Service
info.app.version=1.0.0
```
The response will be:
```json
{
  "app": {
    "version": "1.0.0",
    "description": "Testing Eureka Service",
    "name": "my-service"
  }
}
```
Depending on the version of Actuator, the `/info` endpoint might not be enabled by default to read the variables from the `application.properties` file. To enable it, add the following line to the file:
```properties
management.info.env.enabled=true
```
### Add Actuator to a project:
To add Spring Boot Actuator to your project, you need to include it as a Maven dependency:
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```
After updating the dependencies and running the project, the Actuator endpoints will be ready to use.