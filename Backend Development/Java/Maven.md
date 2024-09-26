Created: 2024-09-26 19:11
## Family Tree:
1. Computer
2. Backend Development
3. [[Java]]
-- -
**Maven** is a tool that helps manage Java projects, handling tasks like compilation, testing, packaging, and deploying the project to a local or remote server. Additionally, Maven automates dependency management (libraries) for the project.
## How Maven Works
Maven revolves around the concept of **POM** files (Project Object Model). A **POM** file represents a project in Maven, containing the minimal configuration required for it to run correctly. The POM file we create inherits from a **Super POM**, meaning we only need to add specific configuration details to customize the project.
### Example POM File:
```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" 
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
   <modelVersion>4.0.0</modelVersion>
   <!-- Organization or team that owns the project -->
   <groupId>com.empresa.project-group</groupId>
   <!-- Unique ID for the project -->
   <artifactId>project</artifactId>
   <!-- Version of the project -->
   <version>1.0</version>
   <!-- Project dependencies -->
   <dependencies>
      <!-- MySQL dependency for database access -->
      <dependency>
         <groupId>mysql</groupId>
         <artifactId>mysql-connector-java</artifactId>
         <version>8.0.16</version>
      </dependency>
      <!-- JUnit dependency for testing -->
      <dependency>
         <groupId>junit</groupId>
         <artifactId>junit</artifactId>
         <version>4.12</version>
         <scope>test</scope> <!-- Scope is test, so it's only used during testing -->
      </dependency>
   </dependencies>
</project>
```
### Key Fields in POM:
- **`groupId`**: Indicates the organization or company and team that owns the project.
- **`artifactId`**: Assigns a unique ID to the project.
- **`version`**: Specifies the version of the project.
### Dependencies:
Inside the `<dependencies>` tag, we list all the dependencies (libraries) the project needs. Maven uses **dependencies** instead of libraries because a dependency can encompass more than just a single library.
Example dependencies:
- **MySQL Connector**: Used to interact with a MySQL database (`mysql-connector-java`).
- **JUnit**: A framework used for unit testing in Java (`junit`).
In Maven, managing these dependencies is automated, and Maven will download them from a central repository, saving time and avoiding manual library configuration.
## Maven Project Lifecycle
1. **Maven Validate**:
   This phase ensures that the project has all the necessary information to be processed correctly. It checks for completeness and correctness in the configuration.
2. **Maven Compile**:
   During this phase, Maven compiles the source code. It transforms the `.java` files into `.class` files and places them in a target directory.
3. **Maven Test**:
   In this phase, unit tests are executed to ensure the correctness of the code. These tests check the functionality of individual components in isolation.
4. **Maven Package**:
   Maven packages the compiled code into a distributable format, such as a **JAR**, **WAR**, or **EAR** file. The most commonly used format is **JAR** (Java Archive).
5. **Maven Verify**:
   This phase runs integration tests to validate the proper functioning of the entire project after it has been compiled and packaged.
6. **Maven Install**:
   The project is installed into the **local repository**. This allows other local projects to use the packaged project as a dependency by referencing it in their POM files.
7. **Maven Deploy**:
   Maven deploys the project to a **remote repository**, making it available to other developers. They can download and use the project by adding it to their dependencies.
### Maven Repositories:
As seen in the `install` and `deploy` phases, Maven sends the project to repositories—either local or remote. **Repositories** are the places where Maven looks for dependencies that are declared in the **POM** file.
- **Local Repository**: A directory on the developer's machine where Maven stores downloaded dependencies and installed projects.
- **Remote Repository**: A shared repository, often used by teams or organizations, where projects are deployed for broader access by other developers or applications.