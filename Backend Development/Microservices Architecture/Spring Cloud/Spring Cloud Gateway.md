Created: 2024-10-04 16:12
## Family Tree:
1. Computer
2. Backend Development
3. Microservices Architecture
4. [[Spring Cloud]]
-- -
Spring Cloud provides a framework called **Spring Cloud Gateway**, which implements the **Edge Server** pattern. It acts as a unified entry point for communication between external systems and an internal microservices ecosystem. This design provides various tools to manage and control this central communication channel, offering significant advantages for microservices-based applications.
## Communication Channels
In the architecture, we observe two types of communication channels:
1. **Public Channel**: Exposed to external systems (such as front-end clients) via **Spring Cloud Gateway** on a public port, typically 8080.
2. **Private/Secure Channel**: Used for internal communication between microservices on non-public ports (different from 8080). This channel is protected from external access, meaning front-end clients cannot invoke microservices directly.
## Key Advantages
- **Cross-cutting Concerns**: The gateway transparently handles common concerns across all microservices. These include:
    - **Monitoring**: Tracking microservice health and performance.
    - **Usage Metrics**: Collecting data on how frequently microservices are accessed.
    - **Authentication and Authorization**: Enforcing security policies before traffic reaches the internal services.
    - **Data Security and Integrity**: Ensuring sensitive data is protected throughout the communication.

- **Abstraction from Microservices**:
    - The client (e.g., a front-end application) does not need to know or directly access individual microservices. The gateway abstracts these services and routes requests based on business logic or specific criteria.
    - It prevents the client from being tightly coupled to specific HTTP addresses, allowing the system to evolve without impacting external systems.

- **Single Access Point**:
    - Clients can access multiple microservices or a combination of their functionalities through a **single unified endpoint** (the gateway). This simplifies the client’s interaction, as they no longer need to connect to multiple services individually to achieve a particular functionality.

- **Dynamic Routing and Load Balancing**:
    - Based on user requests (e.g., URL patterns, session data, or HTTP headers), the gateway can make intelligent decisions regarding which microservice to route the request to.
    - It can also balance traffic between services, improving scalability and efficiency.
## Spring Cloud Gateway
Spring Cloud Gateway is a way to implement the **Edge Server** pattern. It acts as a proxy that grants access only to services created for consumption by external systems outside the microservices ecosystem. This single access point ensures the encapsulation and security of our microservices. Additionally, it allows us to implement business rules common to all requests at the Gateway, such as security or logging of generic information, known as **Cross-Cutting Concerns**.
### Key Concepts:
There are three basic concepts: **Routing (Gateway Handler), Predicate, and Filter**, which work together to control the behavior of the Gateway.
1. **Routing**: Defines the destination for a particular request. It is associated with a URL if it satisfies certain conditions specified by the Predicate and Filter components.
2. **Predicate**: A condition that the request must meet, such as checking whether the request header contains a specific attribute or if the URL path has a particular value.
3. **Filter**: These are instances of Spring Web Filters, which act as interceptors that run before the business logic associated with an endpoint. Filters can modify request and response data, such as interpreting a security token or logging generic information.
### Implementation:
To demonstrate, we will implement a solution based on two microservices: **User** and **Product** services. The architecture will be as follows:
#### Configuration:
First, add the following dependency to your project:
```xml
<dependency>
  <groupId>org.springframework.cloud</groupId>
  <artifactId>spring-cloud-starter-gateway</artifactId>
</dependency>
```
#### Setting up routing in `application.yml`:
The following configuration defines rules in the Gateway based on requests:
```yml
server:
  port: 8080

spring:
  cloud:
    gateway:
      routes:
        - id: productRoute
          uri: http://localhost:8082
          predicates:
            - Path=/product/**
        - id: userRoute
          uri: http://localhost:8081
          predicates:
            - Path=/user/**
```
This sets up routing for the **Product** service on port 8082 and the **User** service on port 8081. The Gateway listens on port 8080 and directs requests based on the URL path.
#### Adding filters:
Next, we'll add filters to the **User** service for modifying request and response headers:
```yml
server:
  port: 8080

spring:
  cloud:
    gateway:
      routes:
        - id: productRoute
          uri: http://localhost:8082
          predicates:
            - Path=/product/**
        - id: userRoute
          uri: http://localhost:8081
          predicates:
            - Path=/user/**
          filters:
            - AddRequestHeader=user-request-header, custom-user-request-header
            - AddResponseHeader=user-response-header, custom-user-response-header
```
#### Handling headers in the User Service:
Modify the **User Service** to handle custom headers:
```java
@RestController
class UserService {
    @RequestMapping(method = RequestMethod.GET, path = "/user/detail/{id}")
    public Map<String, Object> detail(@PathVariable("id") Long idUser, @RequestHeader("user-request-header") String header) {
        Map<String, Object> response = new HashMap<>();
        response.put("id_user", idUser);
        response.put("custom_header_value", header);
        return response;
    }
}
```
#### Testing:
Use **Postman** to send an HTTP request to the **User Service**. The **request header** will return the custom value as part of the response.
#### Creating custom filters:
To log requests and response times, we will implement a custom filter:
```java
@Component
public class LogFilter extends AbstractGatewayFilterFactory<LogFilter.Config> {
    private static Logger log = Logger.getLogger(LogFilter.class.getName());
    public LogFilter() {
        super(Config.class);
    }

    @Override
    public GatewayFilter apply(Config config){
        return (exchange, chain) -> {
            // Log the request path before invoking the real service
            log.info("Path requested: " + exchange.getRequest().getPath());
            return chain.filter(exchange).then(Mono.fromRunnable(() -> {
                // Log the response time after invoking the real service
                log.info("Time response: " + Calendar.getInstance().getTime());
            }));
        };
    }

    public static class Config {
        // Configuration properties
    }
}
```
#### Configuring global filters:
Reference the custom filter in the `application.yml`:
```yml
spring:
  cloud:
    gateway:
      default-filters:
        - name: LogFilter
      routes:
        - id: productRoute
          uri: http://localhost:8082
          predicates:
            - Path=/product/**
        - id: userRoute
          uri: http://localhost:8081
          predicates:
            - Path=/user/**
          filters:
            - AddRequestHeader=user-request-header, custom-user-request-header
            - AddResponseHeader=user-response-header, custom-user-response-header
```
When invoking the **User Service** again using Postman, the console will now show custom logging for both request paths and response times, thanks to the global log filter.
## Security
In microservices design, **Spring Cloud Gateway** is ideal for applying security because of its role as the **Edge Server**—the primary access point for external communication with microservices. Since all incoming requests are funneled through the Gateway, it becomes the natural place to enforce **authentication** and **authorization** mechanisms.
### Authentication vs. Authorization
- **Authentication**: The process of confirming the identity of a user, ensuring they are who they claim to be. This is typically achieved through methods like:
    - Passwords
    - Multi-factor authentication (MFA)
    - IP verification
    - Token-based authentication (such as OAuth or JWT)
- **Authorization**: This process occurs after authentication and verifies if the authenticated user has permission to perform specific actions (like accessing a particular resource). It typically checks the roles and permissions associated with the user’s account.
### Security in Spring Cloud Gateway:
With Spring Cloud Gateway, we can implement security at the **edge** using tools like **Spring Security** combined with **OAuth2** or **JWT (JSON Web Token)** to manage authentication and authorization.
- **Authentication with OAuth2 or JWT**:
  You can configure Spring Cloud Gateway to handle authentication by integrating it with an external **OAuth2 Authorization Server** or using **JWT** tokens passed in the request header.
#### Adding dependencies for security:
To add security to the Gateway, include the following dependencies in your `pom.xml`:
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-oauth2-client</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-security</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.security</groupId>
    <artifactId>spring-security-oauth2-jose</artifactId>
</dependency>
```
#### JWT Token-based authentication example:
In this example, we configure Spring Cloud Gateway to authenticate requests using JWT tokens. The tokens are expected to be included in the `Authorization` header of each request.
##### Configuration in `application.yml`:
```yml
spring:
  security:
    oauth2:
      resourceserver:
        jwt:
          issuer-uri: https://auth-server.com/ # Issuer of the JWT tokens
```
##### Securing Routes:
You can secure individual routes by configuring predicates and applying security filters. Here’s how to configure route-level security:
```yml
spring:
  cloud:
    gateway:
      routes:
        - id: secureRoute
          uri: http://localhost:8081
          predicates:
            - Path=/secure/**
          filters:
            - RemoveRequestHeader=Cookie
            - RemoveResponseHeader=Set-Cookie
```
##### Custom Security Configuration:
You can define custom security rules using **Spring Security** by configuring the Gateway as follows:
```java
@EnableWebFluxSecurity
public class SecurityConfig {

    @Bean
    public SecurityWebFilterChain securityWebFilterChain(ServerHttpSecurity http) {
        http
            .authorizeExchange(exchanges -> exchanges
                .pathMatchers("/secure/**").authenticated()
                .anyExchange().permitAll()
            )
            .oauth2ResourceServer(ServerHttpSecurity.OAuth2ResourceServerSpec::jwt);

        return http.build();
    }
}
```
#### Authorization based on Roles and Permissions:
Authorization can be handled by inspecting the claims inside the JWT token (such as user roles or permissions) to determine whether the user has access to the requested resource.
You can implement **role-based access control (RBAC)** like this:
```java
@EnableWebFluxSecurity
public class SecurityConfig {

    @Bean
    public SecurityWebFilterChain securityWebFilterChain(ServerHttpSecurity http) {
        http
            .authorizeExchange(exchanges -> exchanges
                .pathMatchers("/admin/**").hasRole("ADMIN")
                .pathMatchers("/user/**").hasRole("USER")
                .anyExchange().permitAll()
            )
            .oauth2ResourceServer(ServerHttpSecurity.OAuth2ResourceServerSpec::jwt);

        return http.build();
    }
}
```
Here, requests to `/admin/**` are only accessible to users with the `ADMIN` role, while `/user/**` is accessible to users with the `USER` role.
### Benefits of implementing Security at the Gateway:
- **Centralized Security**: By managing authentication and authorization at the Gateway, you ensure all microservices behind the Gateway are protected by a unified security mechanism.
- **Simplified Microservice Code**: Individual microservices no longer need to implement their own security logic, as it's handled by the Gateway.
- **Cross-Cutting Concerns**: Security can be combined with other cross-cutting concerns, such as monitoring, logging, and rate limiting, within the Gateway itself.
## OAuth 2.0 in Spring Cloud Gateway
### Adding OAuth 2.0 dependency to the Gateway Microservice:
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-oauth2-client</artifactId>
</dependency>
```
### Modifying Spring Configuration:
```yml
spring:
  security:
    oauth2:
      client:
        provider:
          google:
            issuer-uri: https://accounts.google.com
        registration:
          google:
            client-id: your-client-id
            client-secret: your-client-secret
            scope: openid
            redirect_uri: http://localhost:8080/login/oauth2/google
```
### Modifying Gateway Configuration:
```yml
spring:
  cloud:
    gateway:
      default-filters:
        - TokenRelay
```
### Defining Firewall Configuration:
```java
@Configuration
public class SecConfig {
  @Bean
  SecurityWebFilterChain springSecurityFilterChain(ServerHttpSecurity http, ReactiveClientRegistrationRepository clientRegistrationRepository) {
    http.oauth2Login();
    http.logout(logout -> logout.logoutSuccessHandler(new OidcClientInitiatedServerLogoutSuccessHandler(clientRegistrationRepository)));
    http.authorizeExchange().anyExchange().authenticated();
    http.headers().frameOptions().mode(XFrameOptionsServerHttpHeaderWriter.Mode.SAMEORIGIN);
    http.csrf().disable();
    return http.build();
  }
}
```
### Modifying necessary Controllers:
```java
@RestController
@RequestMapping("/account")
public class AccountController {
  @GetMapping("/detail/{id}")
  public Map<String, Object> detail
  (
    @RegisteredOAuth2AuthorizedClient OAuth2AuthorizedClient authorizedClient, 
    Authentication auth,
    @PathVariable("id") Long idAccount
  ) {
    Map<String, Object> response = new HashMap<>();
    response.put("clientName", authorizedClient.getClientRegistration().getClientName());
    response.put("accessToken", authorizedClient.getAccessToken());
    response.put("authName", auth.getDetails());
    response.put("id_account", idAccount);
    return response;
  }
}
```