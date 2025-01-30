Created: 2024-09-17 15:18
## Family Tree:
1. Computer
2. Backend Development
3. Go
4. [[Go Web]]
-- -
Let's break down the process of setting up a Go server using the Gin (Go Web Server > Gin Web Framework) framework that handles `POST` requests and returns a response with an added `ID` to the received product.
## Steps
### Define the Request structure:
We define a struct to match the structure of the incoming JSON request. The `json` tags are used to map the incoming JSON fields to the struct fields.
```go
type request struct {
   ID       int     `json:"id"`       // This will be assigned in the code
   Nombre   string  `json:"nombre"`   // Name of the product
   Tipo     string  `json:"tipo"`     // Type of product
   Cantidad int     `json:"cantidad"` // Quantity
   Precio   float64 `json:"precio"`   // Price
}
```
### Set up the Gin Web Server
We create a Gin web server and set up a `POST` route at `/productos`.
```go
r := gin.Default()           // Create a Gin instance with default middleware
r.POST("/productos", func(c *gin.Context) {   // Define the POST route
    // Handler logic will go here
})
r.Run()  // Start the server (defaults to port 8080)
```
### Binding incoming JSON to the struct:
We use `ShouldBindJSON()` to parse the incoming JSON request and bind it to our `request` struct. If the parsing fails, we return a `400 Bad Request` response with the error.
```go
r.POST("/productos", func(c *gin.Context) {
    var req request   // Initialize a variable to hold the request data
    if err := c.ShouldBindJSON(&req); err != nil {   // Bind incoming JSON to struct
        c.JSON(400, gin.H{  // If there's an error, return 400 with error message
            "error": err.Error(),
        })
        return
    }
    // Handler logic will continue here if the request is successful
})
```
### Add an ID to the Product and return the Response:
If the incoming request is valid, we manually assign an `ID` to the product (in this case, a static value of `4`), and return the updated product as a JSON response with a `200 OK` status.
```go
r.POST("/productos", func(c *gin.Context) {
    var req request
    if err := c.ShouldBindJSON(&req); err != nil {
        c.JSON(400, gin.H{
            "error": err.Error(),
        })
        return
    }

    // Assign an ID to the product
    req.ID = 4

    // Return the modified product as a JSON response with a 200 status
    c.JSON(200, req)
})
```
### Complete code example:
Here is the complete code for the server that handles `POST` requests, assigns an ID, and returns the product:
```go
package main

import (
    "github.com/gin-gonic/gin"
)

type request struct {
    ID       int     `json:"id"`
    Nombre   string  `json:"nombre"`
    Tipo     string  `json:"tipo"`
    Cantidad int     `json:"cantidad"`
    Precio   float64 `json:"precio"`
}

func main() {
    r := gin.Default()

    r.POST("/productos", func(c *gin.Context) {
        var req request

        // Bind the incoming JSON to the request struct
        if err := c.ShouldBindJSON(&req); err != nil {
            c.JSON(400, gin.H{
                "error": err.Error(),
            })
            return
        }

        // Assign an ID to the product
        req.ID = 4

        // Return the product with the assigned ID
        c.JSON(200, req)
    })

    // Start the server on port 8080
    r.Run(":8080")
}
```
## Grouped POST
We define our request structure outside of the main function:
```go
type request struct {
    ID       int     `json:"id"`
    Nombre   string  `json:"nombre"`
    Tipo     string  `json:"tipo"`
    Cantidad int     `json:"cantidad"`
    Precio   float64 `json:"precio"`
}
```
We create a group for products where we will define different endpoints. In our case, we will only have the "save" endpoint.
```go
func main() {
    r := gin.Default()
    pr := r.Group("/productos")
    pr.POST("/", Guardar())
    r.Run()
}
```
Finally, to implement the save functionality, we need to create a function that returns another function with the Gin context as a parameter.
```go
func Guardar() gin.HandlerFunc {
   return func(c *gin.Context) {
       var req request
       if err := c.ShouldBindJSON(&req); err != nil {
           c.JSON(404, gin.H{
               "error": err.Error(),
           })
           return
       }
       req.ID = 4
       c.JSON(200, req)
   }
}
```
## Store in local memory
We will proceed to store all the sent products in memory, as long as the request is correct. The first thing we will do is declare at the global level: A variable for products where the sent products will be stored. A variable that stores and increments the ID, so that the maximum ID is always used.
```go
var products []request
var lastID int
```
Instead of assigning a fixed ID, we increment the ID by 1 and assign it to our product.
```go
lastID++
req.ID = lastID
```
Finally, we store the product with the assigned ID in memory. In this way, they will be saved as we continue making requests.
```go
products = append(products, req)
```