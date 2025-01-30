Created: 2024-09-28 19:02
## Family Tree:
1. Computer
2. Backend Development
3. Java
4. [[Spring Boot]]
-- -
## Handling Multiple Parameters with GET Method
### `@GetMapping`:
In a REST controller, we can handle multiple parameters within a method. For example, in a simple "Hello World" scenario, we can pass parameters such as name, last name, and age using the following code:
```java
@RestController
public class HelloRestController {
   @GetMapping(path = "{name}/{lastname}/{age}")
   public String sayHello(@PathVariable String name, @PathVariable String lastName, @PathVariable Integer age) {
       return "Hola, " + name + " " + lastName + ". Tu edad es: " + age;
   }
}
```
### `@PathVariable`:
This annotation allows us to extract information from the URI itself, rather than treating it as key-value pairs. For example:
```java
@GetMapping("/user/{userId}")
public User getUser(@PathVariable("userId") String userId) {
    // Logic to fetch user
}
```
### `@RequestParam`:
Allows us to handle parameters passed in the query string, such as in the following URL format: `http://localhost:8080/student?name=Horacio&lastname=Quiroga`
Example:
```java
@GetMapping(path = "/student/")
public Student findStudent(@RequestParam String name, @RequestParam String lastName) {
    // Logic to find the student
}
```
## Handle Multiple Parameters with POST Method
### `@PostMapping`:
`@PostMapping` is used to map HTTP POST requests to a method in a controller. It can handle creating new resources like an `Employee` object. Here’s an example of handling multiple parameters in a POST request:
```java
@RestController
@RequestMapping("/")
public class HelloRestController {
   @PostMapping(path = "/employee")
   public void addEmployee(@RequestBody Employee employee) {
       // Logic to add an employee
   }
}
```
### Payload in POST Requests:
When making a POST or PUT request, the request body (payload) can contain data in JSON format, which will be sent to the server. For example:
```json
{
   "firstname": "Charly",
   "lastname" : "Brown",
   "username" : "charlyb",
   "email"    : "charlyb@digitalhouse.com"
}
```
### `@RequestBody`:
The `@RequestBody` annotation binds the HTTP request body to a Java object, allowing automatic deserialization of JSON (or XML) data into a Java class. For example:
```java
public class Employee {
   private Long id;
   private String name;
   private String lastName;
}

@RestController
@RequestMapping("/")
public class HelloRestController {

   @PostMapping(path = "/employee")
   public void handle(@RequestBody Employee employee) {
       // Logic to handle the employee object
   }
}
```
## Sending Responses
### `@ResponseBody`:
The `@ResponseBody` annotation tells Spring to automatically convert a Java object returned by a method into a JSON or XML response. This is especially useful for sending data back to the client. For example:
```java
@GetMapping(path = "/orders/")
@ResponseBody
public List<Order> getOrders() {
   return orderService.getAllOrders();
}
```
In this case, the list of orders will be serialized into a JSON response, as the `@ResponseBody` handles the transformation from Java objects to a format that can be sent via HTTP.