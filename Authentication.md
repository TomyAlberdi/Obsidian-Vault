#Development #Cheatsheet 
In software architecture terms, a [[middleware]] is a component in our applications that allows us to focus on business logic by resolving some low-level complexities.
## Middleware in an HTTP Context
Middleware functions in an HTTP context can serve very broad and varied purposes.
![[image 6.png]]
### Middlewares in [[Go]]:
#### Example 1
```go
func GetDummyEndpoint(c *gin.Context) {
   resp := map[string]string{"hello":"world"}
   c.JSON(200, resp)
}
func main() {
   api := gin.Default()
   api.GET("/dummy", GetDummyEndpoint)
   api.Run(":8080")
}
```
#### Example 2
```go
func DummyMiddleware(c *gin.Context) {
   fmt.Println("I'm a dummy!")
   // Pass on to the next-in-chain
   c.Next()
}
func main() {
   // Insert this middleware definition before any routes
   api.Use(DummyMiddleware)
   // ... more code
}
```
#### Example 3
```go
func DummyMiddleware() gin.HandlerFunc {
   // Do some initialization logic here
   // Foo()
   return func(c *gin.Context) {
       c.Next()
   }
}
func main() {
   // ...
   api.Use(DummyMiddleware())
   // ...
}
```
## API Authentication Middleware
If we're creating an API with [[Go Web Server#Gin Web Framework|Gin]], we probably want to add some kind of authentication mechanism. The simplest solution is to check if the client sends us a URL parameter, like `api_token`, and then validate it to allow the request to proceed.
```go
func TokenAuthMiddleware() gin.HandlerFunc {
   requiredToken := os.Getenv("API_TOKEN")
   return func(c *gin.Context) {
       token := c.GetHeader("api_token")

       if token != requiredToken {
           c.AbortWithStatusJSON(401, gin.H{"error": "Invalid API token"})
           return
       }    
       c.Next()
   }
}
```