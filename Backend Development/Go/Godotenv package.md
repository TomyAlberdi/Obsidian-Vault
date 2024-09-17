Created: 2024-09-17 15:01
## Family Tree:
1. Computer
2. Backend Development
3. [[Go]]
-- -
**Godotenv** is a Go package used to load and read environment variables (Working Environments > Environment Variables) from a `.env` file. To configure environment variables, we use `.env` files, colloquially called "dotfiles."
In the Go ecosystem, we also have some alternatives for working with this type of file. One of them is the **godotenv** library, which is a port of its Ruby version.
## Installation
To install the **godotenv** package, run the following command in the console:
```bash
go get -u github.com/joho/godotenv
```
To use it in the root of our project, create a file named `.env`. For example:
```go
MY_USER=username
MY_PASSWORD=pass
```
## Usage
With **godotenv** installed and the file created, you just need to import it into your Go application and use it.
```go
package main

import (
   "github.com/joho/godotenv"
   "log"
   "os"
)

func main() {
   err := godotenv.Load()
   if err != nil {
      log.Fatal("Error loading .env file")
   }

   user := os.Getenv("MY_USER")
   password := os.Getenv("MY_PASSWORD")
}
```
## Token in Environment Variable:
Example of token validation.
```go
func (c *Product) GetAll() gin.HandlerFunc {
   return func(ctx *gin.Context) {
       token := ctx.GetHeader("token")

       if token != os.Getenv("TOKEN") {
           ctx.JSON(401, gin.H{"error": "invalid token"})
           return
       }

       p, err := c.service.GetAll()
       ...
   }
}
```
`ctx.GetHeader` allows you to retrieve variables from the request header. It does **not** allow fetching variables stored in a `.env` file.