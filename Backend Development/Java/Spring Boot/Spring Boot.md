Created: 2024-09-28 00:27
## Family Tree:
1. Computer
2. Backend Development
3. [[Java]]
-- -
## Spring
**Spring** is an open-source framework for building Java applications. It has a modular structure and offers great flexibility to implement different types of architectures based on the applicatrion's needs.
**Spring Boot**, on the other hand, is an extension of Spring. It's a pre-configured suite that allows you to run Spring applications using best practices while still retaining flexibility. Spring Boot's design philosophy is to offer an opinionated approach to how the Spring framework should be implemented, maintaining a clean architecture and following best practices.
### What can Spring do?
- **Microservices**: Easily deploy new functionalities independently.
- **Reactive**: Spring's asynchronous architecture allows better use of computing resources.
- **Cloud**: Enables coding for any cloud platform and helps scale applications.
- **Web Applications**: Allows building fast, secure, and responsibe web applications while connecting to any database using ORM technologies.
- **Serverless**: Supports building serverless applications that respond to business events.
- **Event-Driven**: Enables creating applications that react to business events.
- **Batch Processing**: Automates online and offline process flows.
### Spring Platform:
Spring Platform is a suite of open-source projects developed in Java aimed at streamlining application development. It offers tools for data access, infrastructure, web applications, microservices, and more.
Some key projects include:
- Spring Boot
- Spring HATEOAS
- Spring Framework
- Spring REST Docs
- Spring Data
- Spring Batch
- Spring Cloud
- Spring Security
- Spring for Apache Kafka
- Spring Web Flow
## Spring Boot
As previously mentioned, **Spring Boot** is an extension of the Spring framework, enabling the quick and easy creation of production-ready web applications with a "just run" philosophy. It requires minimal configuration and integrates with many Spring Platform projects and third-party libraries, reducing development time and boosting productivity.
### Key features:
1. **Embedded Web Server**:
   Spring Boot includes an embedded Tomcat server by default (also supports Jetty and Undertow) without requiring prior installation.
2. **Default Port 8080**:
   The embedded server listens to HTTP requests on port `8080` by default. You can access your app at `http://localhost:8080/` after starting the server. You can configure a different port and other properties via the `application.properties` file.
3. **Spring Boot Starters**:
   Starters limit the amount of manual dependency configuration. These are Maven dependencies defined in the `POM.xml` file. Spring Boot handles the dependencies, ensuring compatibility within the application. The starters typically start with `spring-boot-starter-*`, where `*` represents the type of application to be developed.
	- **spring-boot-starter-web**: For developing RESTful web services with Spring MVC and Tomcat as the embedded container.
	- **spring-boot-starter-jdbc**: For JDBC connection pooling, built on Tomcat's JDBC connection pool implementation.
4. **Spring Boot Initializr**:
   A web utility that helps generate a skeleton Spring Boot project with the desired configurations (dependency manager, language, packaging type, dependencies, etc.). It can be used via its official website or integrated into IDEs like IntelliJ IDEA.
### Project Structure:
When a Spring Boot project is created, it generates several files and directories, such as:
- `pom.xml` (for Maven dependencies)
- `application.properties`
- `target` folder (after building the project)
- `profile` folder (for defining environments)
![[Backend Development/Java/Spring Boot/attachments/image.png]]
### Annotations:
Spring Boot minimizes configuration through **annotations**, which provide metadata to the compiler or development tools. An annotation is placed before a class, method, or declaration and looks like `@Annotation`. For example:
```java
@Author(name = "DH", date = "14/03/2022")
public class ExampleClass() {}
```
You can also use multiple annotations:
```java
@Author(name = "DH", date = "14/03/2022")
@Deprecated
@AnotherAnnotation("value")
public class ExampleClass() {}
```
#### Common annotations:
- `@Deprecated`: Indicates that a method is obsolete and will be removed in the future.
- `@Override`: Tells the compiler that a method is overriding a method from its parent class.
- `@SuppressWarnings`: Instructs the compiler to suppress certain warnings, useful when you want to ignore known issues.
### Main Class:
In Java, every application must have a main class with a `main` method. In Spring Boot, the main method calls the `run` method of the `SpringApplication` class to start the application. Here's an example of how to define the main class of a Spring Boot application:
```java
@Configuration
@EnableAutoConfiguration
@ComponentScan
public class Application {
  public static void main(String[] args) throws Exception {
    SpringApplication.run(Application.class, args);
  }
}
```
To simplify, **Spring Boot** allows you to replace the three annotations (`@Configuration`, `@EnableAutoConfiguration`, and `@ComponentScan`) with a single annotation:
```java
@SpringBootApplication
public class Application {
  public static void main(String[] args) throws Exception {
    SpringApplication.run(Application.class, args);
  }
}
```