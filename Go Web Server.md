#Development 
## Package `net/http`
This package allows you to create web servers in a simple way. A fundamental concept in net/http servers is the use of handlers. A handler is an object that implements the `http.Handler` interface. A common way to write a handler is by using the `http.HandlerFunc` adapter in functions with the appropriate signature.
Functions that serve as handlers take an `http.ResponseWriter` and an `http.Request` as arguments. The Response Writer is used to return the HTTP response.
In the following example, our response is simply "Hello World":
```go
func helloWorld(w http.ResponseWriter, req *http.Request) {
  fmt.Fprintf(w, "Hello World\n")
}
```
We register our handlers on server routes using the `http.HandleFunc` function. We set up the default router in the `net/http` package and pass a function as an argument.
Finally, we call `ListenAndServe` with port ":8080" and a handler. Passing `nil` tells it to use the default router that we just configured.
```go
func main() {
  http.HandleFunc("/hello", helloWorld)
  http.ListenAndServe(":8080", nil)
}
```
We run the web server with the following command: `go run main.go`.
To test our endpoint, we go to the following URL: [http://localhost:8080/hello](http://localhost:8080/hello).
## Gin Web Framework
Just as we can create a server using the `net/http` package, there are other frameworks that allow us to build a web server.
Gin is a high-performance microframework that can be used to create web applications and microservices in [[Go]]. It includes a set of features (e.g., routing, middleware, rendering, etc.) that reduce repetitive code and simplify the creation of web applications and microservices.
### How it works:
Let’s quickly go over how Gin processes a request. The control flow for a typical web application, API server, or microservice is as follows:
1. Request.
2. Router.
3. Middleware.
4. Route Handler.
5. Middleware.
6. Response.
When a client request arrives, Gin first analyzes the route. If a matching route definition is found, Gin invokes the middlewares (which are optional) in the order defined by the route definition (if any), followed by the route handler.
### Getting Gin:
To use Gin, Go version 1.13+ is required. Once installed, use the following command to install Gin:
```bash
go get -u github.com/gin-gonic/gin
```
Then import it into your code:
```go
import "github.com/gin-gonic/gin"
```
### Creating a Web Server:
1. **Create a repository on GitHub.**
2. After creating the repository, clone it and open it in your IDE.
3. Initialize your module with the following command:
```go
   go mod init github.com/username/webserver
```
The domain and module name should match the name of the module already created.
4. Once Gin is installed, we can create a simple web server. The `gin.Default()` function creates a Gin router with two default middlewares: `logger` and `recovery`.
```go
   router := gin.Default()
```
5. With the router defined, we can start adding the various endpoints that our application will have. To do this, we add different handlers to the router.
   Here’s an example where we create a handler using the `router.GET("endpoint", Handler)` function, where `endpoint` is the relative path, and `handler` is a function that takes `*gin.Context` as an argument.
   In the following example, the handler function serves a JSON response with a 200 status:
```go
	router.GET("/hello-world", func(c *gin.Context) {
	  c.JSON(200, gin.H{
		"message": "Hello World",
	  })
	})
```
6. Lastly, we start the router using `router.Run()`, which by default listens on port 8080:
```go
   router.Run()
```
7. To run our application, we use the following command:
```bash
   go run main.go
```
To test our endpoint, go to the URL [http://localhost:8080/hello-world](http://localhost:8080/hello-world). You should receive the specified JSON response.
#### Grouped endpoints:
```go
func main() {
  server := gin.Default()
  server.GET("/",welcome)
  // Agrupamos los endpoints referidos al perfil
  gopher := server.Group("/profile")
  {
    gopher.GET("/data", profileData)
    gopher.GET("/friends", profileFriends)
  }
  server.Run(":8080")
```