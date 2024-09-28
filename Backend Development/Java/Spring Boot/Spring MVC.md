Created: 2024-09-28 01:09
## Family Tree:
1. Computer
2. Backend Development
3. Java
4. [[Spring Boot]]
-- -
Spring MVC is a module within the Spring Framework that follows the **Model-View-Controller** design pattern. It helps build web applications by separating concerns between the presentation (View), logic (Controller) and data access (Model) layers.
**How does Spring MVC works?**
Spring MVC relies on a component called `DispatcherServlet`. This component acts as the **front controller**, responsible for delegating and coordinating control between different interfaces during the excecution phase of an HTTP request, using the **Front Controller design pattern**.
This means that all incoming requests to a resource in a Spring MVC application are first handled by a single controller (`DispatcherServlet`), which then forwards the request to the appropiate controller for further processing.
The `DispatcherServlet` may use additional helpers to forward the request appropiately.
## `DispatcherServlet` workflow
1. `HandlerMapping`:
   After receiving an HTTP request, the `DispatcherServlet` queries `HandlerMapping`, which, based on the requested URL, determines which controller should handle the request.
2. `Controller`:
   The selected controller processes the request, calling/executing the appropiate methods (e.g,., GET or POST). After executing the business logic, it return the logical view name to be displayed to the `DispatcherServlet`.
3. `ViewResolver`:
   The `DispatcherServlet` uses `ViewResolver` to map logical view names to the actual physical views (e.g,., JSP, Thymeleaf, etc).
4. `View`:
   Finally, the `DispatcherServlet` forwards the request to the view, which renders the results to the user.
**Presentation Layer Technologies supported by Spring MVC**
Spring MVC supports many types of views (templates) to display the model's data, including:
- **Freemarker**
- **Jackson**
- **JSTL**
- **Velocity**
- **Thymeleaf**
- **JSP**
- **XML**
- **PDF**
- **Excel**
- **Groovy**
## Spring Boot MVC
Spring Boot extends Spring MVC, providing a way to quickly create production-ready applciations with minimal configuration.
### Defining a Controller in Spring Boot:
In Spring Boot MVC, the `@Controller` annotation indicates that a specific class is acting as a controller. The controller serves as an intermediary between the user interface and the business logic, processing requests, and detemrining which view to display.
Key responsibilities of the controller:
- Retrieve HTTP parameters (if any).
- Trigger the business logic.
- Place results ina scope accesible to the view and forward control to the view.
#### Example: Mapping a URL to a Controller
Imagine we type `https://localhost:8080/hello` in the browser.
```java
@Controller
@RequestMapping("/hello")
public class HelloController {
  
  @RequestMapping(method = RequestMethod.GET)
  public String printHello(ModelMap model) {
    model.addAttribute("message", "Hello Spring MVC Framework!");
    return "hello";  // Refers to the hello.html view
  }
}
```
- **`@Controller`**: Defines `HelloController` as a Spring MVC controller.
- **`@RequestMapping("/hello")`**: Maps the URL `/hello` to this controller.
- **`@RequestMapping(method = RequestMethod.GET)`**: Specifies that this method handles **GET** requests. If the same URL is accessed via POST, a 404 error will occur unless POST handling is defined.
- **`return "hello"`**: The logical view name (e.g., `hello.html`).
#### Retrieving URL Parameters:
URL parameters follow the format `key=value` and are joined by `&`. For example:
```
http://example.com/listaOfertas?mes=1&user=google
```
To retrieve URL parameters, use the `@RequestParam` annotation:
```java
@Controller
public class ListaOfertasController {
  @RequestMapping(value = "/listaOfertas", method = RequestMethod.GET)
  public String procesar(Model model, @RequestParam("mes") int mes) {
    model.addAttribute("message", "Hello Spring MVC Framework!");
    model.addAttribute("mes", mes);
    return "ofertas";
  }
}
```
- **`@RequestParam("mes")`**: Binds the HTTP parameter `mes` to the Java parameter `mes`. In the example URL, `mes=1`, so the value `1` is passed to the method.
### Newer annotations in Spring Boot:
Starting from **Spring 4.3**, additional annotations were introduced to simplify handling of different HTTP methods:
- **`@GetMapping`**
- **`@PostMapping`**
- **`@PutMapping`**
- **`@DeleteMapping`**
These annotations help reduce the verbosity of `@RequestMapping`.
Example with `@GetMapping` and `@PostMapping`:
```java
@Controller
public class HelloController {
  @GetMapping("/hello")
  public String printHello(Model model) {
    model.addAttribute("message", "Hello Spring MVC Framework!");
    return "hello";  // View name
  }

  @PostMapping("/guardar")
  public String guardarProducto(@RequestBody Employee employee) {
    return "You have made a POST request";
  }
}
```
- **`@GetMapping("/hello")`**: Maps the GET request for `/hello` to this method.
- **`@PostMapping("/guardar")`**: Maps the POST request for `/guardar` and expects a request body (`@RequestBody Employee employee`).