Created: 2024-10-03 16:52
## Family Tree:
1. Computer
2. Backend Development
3. Microservices Architecture
4. [[Spring Cloud]]
-- -
## Configuration problem
As organizations grow in scale, they start developing atomic microservices that support various business processes. These microservices provide infrastructure, processing, and data support and require different types of configurations to function properly. Some examples of configuration needs include:
- **Localization of other microservices**
- **Paths to databases** and the endpoints of deployed services
- **IP addresses of storage servers** like FTP or S3
- **Logging configuration** (e.g., Log4j settings like INFO, ERROR, DEBUG)
- **Passwords and secrets** (often secured with additional security measures)
- **Environment variables**
**Why can't configuration be hardcoded into the application?**
1. **Decoupling configuration from code**:
   A developer doesn’t need to know the production database URL, passwords, or other general configurations, which are typically managed by the infrastructure or DevOps team. For example, if the infrastructure team changes an internal URL, it doesn’t make sense to ask each development team to redeploy the application. Systems should be able to react to configuration changes without requiring full redeployment.
2. **Separation of environments (Prod, QA, Dev)**:
   Organizations typically have at least three environments:
	1. **Production (Prod)**: The live system where end users interact with the application.
	2. **Quality Assurance (QA)**: Where the QA team tests the code.
	3. **Development (Dev)**: Where the development team works on code.
   Each environment requires its own configuration. While handling this with files can work for small setups, as the number of microservices and configurations grows, it becomes necessary to **centralize configurations**.
3. **Avoiding deploys for configuration changes**:
   Consider a scenario where configurations are embedded directly into the code. Some configurations remain stable for years, while others may change weekly or even daily. If configurations are hardcoded, any configuration change requires a redeployment of the application. However, **separating configuration from code** allows systems to adjust to configuration changes with only a restart, saving time.
   For example:
	- **Deployment time**: 6 minutes per instance
	- **Restart time**: 2 minutes
### Example: Environment-Specific Configurations:
Imagine you are developing a feature for **transferring money between accounts** and need to update the account balances using an account service:
- You need a stable **account service** to verify that the transfer operation works and that balances are updated properly.
- If you only have the account service in a real production environment, you might end up affecting real user accounts—an unacceptable error.
This illustrates why it’s crucial to have **multiple environments** (Dev, QA, Prod) with their own infrastructure, services, databases, and resources to test and operate the system safely.
In a transfer operation, for instance, moving $100 from Account A to Account B should result in Account B having $100 more and Account A having $100 less. Let’s visualize this:
![[Computer Science/Backend Development/Microservices Architecture/Spring Cloud/attachments/image 2.png]]
The transfer service connects to different account services based on the environment (Dev, QA, Prod), and these configurations should not be hardcoded but **externally configured**.
### Why Hardcoding Configurations is a problem:
If the configuration (such as the URL of the account service) were hardcoded into the transfer service, you would need to recompile the project for every deployment to each environment. This significantly increases the **Time to Market (TTM)**, which refers to the time it takes to bring a new feature to production, adding unnecessary delays.
By **externalizing configurations**, you can avoid redeploying applications just to change a URL or environment-specific setting, leading to more efficient development and operational processes.
## Spring Cloud Config: Manage Microservice Configurations with Git
Spring Cloud Config provides a framework that simplifies the management of configurations for microservices and environments. It consists of two main components: **Spring Cloud Config Server** and **Spring Cloud Client**, which interact with each other to manage configurations effectively. Here's an overview of how to integrate Spring Cloud Config with Git to handle distributed configurations:
![[Computer Science/Backend Development/Microservices Architecture/Spring Cloud/attachments/image 3.png]]
### Configuring Values in Git:
The configurations for our microservices are specified as **YML files** in a **GitHub repository**. Each microservice that needs external configuration has its own YML file. Git is commonly used because it provides:
- **Version control**
- **Automatic approval/rejection rules**
- **Easy tracking, application, and reversal of changes**
- **Traceability of changes**
For example, the following files may be present in the repository:
- `application.yml`: Contains general configurations for all services.
- `cuenta-service.yml`: Contains configurations for the `cuenta-service` microservice.
- `transaccion-service.yml`: Contains configurations for the `transaccion-service` microservice.
Let’s modify the `cuenta-service.yml` file as follows:
```yml
server:
  port: ${PORT:8889}
message: "custom configuration with Spring Cloud Config"
```
### Configuring the Config Server:
Once the Git repository is set up with the necessary configurations, we need to create the **Config Server**, which fetches configurations from Git and exposes them via REST services for other microservices.
Steps to set up the config server:
#### Add Spring Cloud Config Dependency:
Add the following dependency to your `pom.xml`:
```xml
<dependency>
  <groupId>org.springframework.cloud</groupId>
  <artifactId>spring-cloud-config-server</artifactId>
</dependency>
```
#### Enable Config Server in the Main Class:
In the Spring Boot startup class, add the `@EnableConfigServer` annotation to indicate that the application will act as a Config Server:
```java
@EnableConfigServer
@SpringBootApplication
public class ConfigServerApplication {
  public static void main(String[] args) {
    SpringApplication.run(ConfigServerApplication.class, args);
  }
}
```
#### Configure the Git source in `application.yml`:
In the `application.yml` file, specify the Git repository URL where the configurations are stored:
```yml
server:
  port: ${PORT:8888}
spring:
  application:
    name: config-server
  cloud:
    config:
      server:
        git:
          uri: https://github.com/user/spring-cloud-example
```
### Validation:
To validate that the Config Server is correctly set up, we can query the configuration of any declared service via HTTP. The request follows this pattern:
```
http://{config-server-url}/{service-name}/{profile-name}
```
- **config-server-url**: The address of the Config Server (running Spring Cloud Config).
- **service-name**: The name of the microservice whose configuration is being queried.
- **profile-name**: The name of the configuration profile to query (we'll discuss this in more detail later).
For example, if we access the following URL:
```
http://localhost:8888/cuenta-service/profile
```
We will see the configuration for the `cuenta-service` if everything is set up correctly.
### Configuring Spring Cloud Config Clients:
To configure a Spring Cloud Config client (a microservice that consumes configurations from the Config Server):
#### Add the Spring Cloud Config Client Dependency:
Add the following dependency to the `pom.xml`:
```xml
<dependency>
  <groupId>org.springframework.cloud</groupId>
  <artifactId>spring-cloud-starter-config</artifactId>
</dependency>
```
#### Set Up `bootstrap.yml`:
Create a `bootstrap.yml` file that specifies the microservice name (used to retrieve its configuration from the Config Server) and the Config Server URL:
```yml
spring:
  application:
    name: cuenta-service
  cloud:
    config:
      url: ${CONFIG_SERVER:http://localhost:8888}
```
#### Add REST Endpoint:
To show the retrieved configurations from the Config Server, add a REST endpoint to the microservice. Add the following dependencies to the `pom.xml`:
```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-web</artifactId>
</dependency>
<dependency>
  <groupId>org.springframework.cloud</groupId>
  <artifactId>spring-cloud-starter-bootstrap</artifactId>
</dependency>
```
Next, create a REST controller to display the configuration values retrieved from Git:
```java
@RestController
class AccountService {
  @Value("${message}")
  private String message;
  
  @Value("${global-message}")
  private String globalMessage;

  @RequestMapping(method = RequestMethod.GET, path = "/service")
  public Map<String, String> getMessage() {
    Map<String, String> response = new HashMap<>();
    response.put("message", message);
    response.put("global-message", globalMessage);
    return response;
  }
}
```
#### Accessing the Service:
Finally, access the `cuenta-service` microservice by navigating to the following URL:
```
http://localhost:8889/service
```
This URL displays the values configured in the Git repository for this service.