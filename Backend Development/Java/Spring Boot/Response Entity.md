Created: 2024-09-28 20:18
## Family Tree:
1. Computer
2. Backend Development
3. Java
4. [[Spring Boot]]
-- -
In Spring, we often have multiple ways to achieve the same goal, including fine-tuning HTTP responses.
## `ResponseEntity`
`ResponseEntity` extends from the `HttpEntity` class and adds an `HttpStatus` or status code. It is typically used in REST services within controller methods.
`ResponseEntity` manages the entire HTTP response, including the body, headers, and status codes, giving us full control over the response we want to send from our endpoints.
Since the parameter type is generic, we can do the following:
```java
@GetMapping("/hello")
ResponseEntity<String> helloWorld() {
    return new ResponseEntity<>("Hello World from an HTTP response!", HttpStatus.OK);
}
```
This allows us to return a `String` as the body type, along with a **200 OK** status code in the response.
Now, let's program an endpoint to return a **400 Bad Request** status code in case an invalid email is entered:
```java
@GetMapping("/verify/{email}")
ResponseEntity<String> verifyEmail(@PathVariable String email) {

  if (!EmailValidator.getInstance().isValid(email)) {    
    return new ResponseEntity<>("Format should be: example@domain.com", HttpStatus.BAD_REQUEST);
  }

  return new ResponseEntity<>("Your email is: " + email, HttpStatus.OK);
}
```
Additionally, we can set a custom response header as follows:
```java
@GetMapping("/header/{client}")
ResponseEntity<String> customHeader(@PathVariable String client) {

  HttpHeaders headers = new HttpHeaders();
  headers.add("Client Status", "Client " + client + ": enabled"); 

  return new ResponseEntity<>("Welcome " + client, headers, HttpStatus.OK);
}
```
### Static Methods in `ResponseEntity`:
`ResponseEntity` also provides two nested interface types: **BodyBuilder** and **HeadersBuilder**. `ResponseEntity` has static methods that allow us to access these interfaces.
Example: "Hello World"
```java
@GetMapping("/helloWorld")
ResponseEntity<String> helloWorld2() {
  return ResponseEntity.ok("Hello World!");
}
```
Example: "Email Validation"
```java
@GetMapping("/verifyEmail/{email}")
ResponseEntity<String> verifyEmail2(@PathVariable String email) {

  if (!EmailValidator.getInstance().isValid(email)) {    
    return ResponseEntity.badRequest().body("Error! Correct format: example@domain.com");
  }

  return ResponseEntity.status(200).body("Email: " + email);
}
```
Example: Custom header
```java
@GetMapping("/customHeader/{client}")
ResponseEntity<String> customHeader2(@PathVariable String client) {

  return ResponseEntity.ok().header("Client Status", "Client " + client + ": enabled").body("Welcome client: " + client);
}
```
## Alternatives
### `@ResponseBody`:
In traditional Spring MVC applications, endpoints generally return rendered HTML pages. However, sometimes we only need to return the actual data, not an HTML page. In such cases, we can annotate the controller method with `@ResponseBody`. This tells Spring to treat the return value of the method as the HTTP response body itself.
### `@ResponseStatus`:
When an endpoint successfully processes a request, Spring automatically provides an HTTP **200 (OK)** response. However, if the endpoint throws an exception, Spring searches for an exception handler that determines which HTTP status to use. We can annotate methods with `@ResponseStatus` to specify a custom HTTP status code to be returned.
### Directly manipulating the Response:
Spring also allows us to directly manipulate the `javax.servlet.http.HttpServletResponse` object. You simply need to declare it as a method parameter, as shown in the following code:
```java
@GetMapping("/manual")
void manual(HttpServletResponse response) throws IOException {
    response.setHeader("Custom-Header", "foo");
    response.setStatus(200);
    response.getWriter().println("Hello World!");
}
```
In this example:
- We manually set a custom header (`Custom-Header`).
- We explicitly set the status code to **200 OK**.
- We write "Hello World!" directly to the response body using `response.getWriter().println()`.