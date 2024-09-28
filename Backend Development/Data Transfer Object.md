Created: 2024-09-28 19:47
## Family Tree:
1. Computer
2. [[Backend Development]]
-- -
One of the most common challenges when developing applications is designing how data should travel from the service layer (or controller) to the application or presentation layer. Often, due to a lack of knowledge, we use **entity classes** to return data. This can lead to returning more data than necessary or requiring multiple calls to the service layer to retrieve all the required information.
To address this issue, the **DTO (Data Transfer Object) pattern** is used.
## Overview
The purpose of the DTO pattern is to create a **plain object (POJO)** with a set of attributes that can be sent to or retrieved from the server in a single call. A DTO can combine information from multiple sources or tables into a single simple class.
### Mapping Data from two entities to a DTO:
Graphically, we can visualize how a DTO is composed of various attributes, which may come from more than one data source. For example, the server retrieves information from the `customer` and `address` tables and maps it to a DTO.
![[Backend Development/attachments/image.png]]
- Some information is passed directly, such as the data from individual fields.
- Other information is derived from multiple fields. For instance, the `fullName` field in the DTO is a combination of `firstname` and `lastname`.
![[Backend Development/attachments/image 1.png]]
One of the main advantages of a DTO is that it allows us to **omit information** that the user doesn’t need. For example, in a DTO, the **password** field is omitted. This is not just unnecessary for the user, but sending passwords in the response could be a security risk, which is why it's left out of the DTO.
## Entities vs DTO
A common mistake is using **entity classes** to transfer data between the client and server. However, entities are designed for **mapping against the database**, not for being a view for a screen or a specific service. This leads to several issues:
- **Entities may not be serializable** or may not contain all the required fields for data transfer.
- To meet data transfer requirements, developers might add more attributes to entity classes, but this dilutes the true purpose of the entity, which is to represent database tables.
This approach leads to a **mixing of entities and DTOs**, which can cause design problems. By using **DTOs**, you can cleanly separate the database mapping (handled by entities) from the data transfer logic (handled by DTOs).
## Read-Only vs Serializable
### Read-Only DTOs:
Since the purpose of a **DTO** is to act as a data transfer object between the client and server, it’s important to avoid having business logic or methods that perform calculations on the data. As a best practice, DTOs should only contain **getter and setter methods** for their respective attributes. This ensures that the DTO is used solely for data transfer and not for modifying or processing the data.
### Serializable DTOs:
When objects need to travel over the network, they must implement the **`Serializable`** interface, both for the class itself and all the attributes it contains. This allows the object to be converted into a format that can be transmitted and reconstructed on the receiving end.
A common mistake in Java is using **`Date`** or **`Calendar`** types to transmit date or time information. These types do not have a standardized serialization format, particularly when used in **Web Services** or **RESTful APIs**. A better approach is to use types like **`String`** (formatted as a date) or **`LocalDate`/`LocalDateTime`** (from Java 8+), which are easier to serialize in a consistent way.
## Jackson
**Transfering Data from an Entity to a DTO**:
One possible solution would be to manually use **getter and setter methods** to assign each field to the DTO object one by one. However, this can be very time-consuming, and as we add new attributes to the classes, it results in more and more code.
There are several libraries that assist with this mapping task by automatically assigning values from an entity to a DTO, and vice versa. One of the most widely used libraries is **Jackson**.
### Example:
Add the dependency to the **POM**:
```xml
<dependency>
   <groupId>com.fasterxml.jackson.core</groupId>
   <artifactId>jackson-databind</artifactId>
   <version>2.9.9</version>
</dependency>
```
User Entity:
```java
public class User {

   private Integer id;
   private String username;
   private String firstName;
   private String lastName;
   private String ssn;
   private String password;

   public User(Integer id, String username, String firstName, String lastName, String ssn, String password) {
       this.id = id;
       this.username = username;
       this.firstName = firstName;
       this.lastName = lastName;
       this.ssn = ssn;
       this.password = password;
   }

   // Getters and Setters
}
```
User DTO:
```java
import com.fasterxml.jackson.annotation.JsonIgnoreProperties;

@JsonIgnoreProperties(ignoreUnknown = true)
public class UserDTO {
   private String username;
   private String firstName;
   private String lastName;

   public UserDTO(String username, String firstName, String lastName) {
       this.username = username;
       this.firstName = firstName;
       this.lastName = lastName;
   }

   // Getters and Setters
}
```
The **`@JsonIgnoreProperties(ignoreUnknown = true)`** annotation tells Jackson to ignore any attributes in the entity that are not present in the DTO. For example, it will ignore the `id` field.
Additionally, Jackson requires that we have an **empty constructor** in the DTO.
### Data Mapping:
```java
@Test
public void entityToDTO() {
   User user = new User(1, "user99", "John", "Doe", "12345678", "abcd1234");
   ObjectMapper mapper = new ObjectMapper();
   UserDTO userDTO = mapper.convertValue(user, UserDTO.class);
   Assert.assertNotNull(userDTO);
}
```
As we can see, all we need to do is create an instance of **`ObjectMapper`** and use the `convertValue` method. This method takes two parameters:
1. The **entity** (in this case, `user`).
2. The **type** to which the data should be converted (in this case, `UserDTO`).
The result is an automatic conversion of the entity to the DTO without manually mapping each field.