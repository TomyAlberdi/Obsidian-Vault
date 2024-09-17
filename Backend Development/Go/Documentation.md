Created: 2024-09-17 15:00
## Family Tree:
1. Computer
2. Backend Development
3. [[Go]]
-- -
## Swagger
To implement Swagger in Go, we will use **Swaggo**, which allows us to generate project Programming Theory/Documentation using comments within the code.
### Installation:
To install the necessary Swaggo packages, run the following commands:
```shell
go get -u github.com/swaggo/swag/cmd/swag
go get -u github.com/swaggo/files
go get -u github.com/swaggo/gin-swagger
```
Add the Go binary path to your environment variables:
```env
export PATH=$PATH:$HOME/go/bin
```
### Global annotations for the Application:
Above the `main` function, add the following annotations to specify and document your application globally:
```go
// @title Certified Tech Developer
// @version 1.0
// @description This API Handles Products.
// @termsOfService https://developers.ctd.com.ar/es_ar/terminos-y-condiciones

// @contact.name API Support
// @contact.url https://developers.ctd.com.ar/support

// @license.name Apache 2.0
// @license.url http://www.apache.org/licenses/LICENSE-2.0.html
```
### Annotations for Controllers:
#### `GetAll` Method:
Above the `GetAll` method in the controller, add the following annotations to document the endpoint:
```go
// ListProducts godoc
// @Summary List products
// @Tags Products
// @Description Get products
// @Accept  json
// @Produce  json
// @Param token header string true "token"
// @Success 200 {object} web.Response
// @Router /products [get]
func (c *Product) GetAll() gin.HandlerFunc {}
```
#### `Store` Method:
Similarly, above the `Store` method, add the annotations to document the endpoint:
```go
// StoreProducts godoc
// @Summary Store products
// @Tags Products
// @Description Store products
// @Accept  json
// @Produce  json
// @Param token header string true "token"
// @Param product body request true "Product to store"
// @Success 200 {object} web.Response
// @Router /products [post]
func (c *Product) Store() gin.HandlerFunc {}
```
### Generate Documentation:
To generate the documentation, use the Swaggo command and specify where the `main.go` file is located:
```sh
swag init -g cmd/server/main.go
```
Once the command is executed, Swaggo will generate a `docs` package containing all the project documentation based on the comments.
### Viewing the Documentation:
To visualize the documentation, we will use the **gin-swagger** package, which helps display the documentation from within Gin.
#### Package Imports:
Import the necessary packages for viewing the documentation from an endpoint:
```go
"github.com/ncostamagna/meli-bootcamp/docs"
"github.com/swaggo/files"
ginSwagger "github.com/swaggo/gin-swagger"
```
Make sure to add the `HOST` environment variable to your `.env` file with the base URL of the application:
```
HOST=localhost:8080
```
### Main Program:
In the `main` function, add the endpoint for the generated documentation and set the `HOST` value from the environment variable:
```go
func main() {
   _ = godotenv.Load()
   db := store.New(store.FileType, "./products.json")
   repo := products.NewRepository(db)
   service := products.NewService(repo)
   p := handler.NewProduct(service)
   r := gin.Default()

   docs.SwaggerInfo.Host = os.Getenv("HOST")
   r.GET("/docs/*any", ginSwagger.WrapHandler(swaggerFiles.Handler))

   pr := r.Group("/products")
   pr.POST("/", p.Store())
   pr.GET("/", p.GetAll())
   pr.PUT("/:id", p.Update())
   pr.PATCH("/:id", p.UpdateName())
   pr.DELETE("/:id", p.Delete())
   r.Run()
}
```
### Accessing the Documentation:
Once your server is running, you can view the Swagger documentation by navigating to:` http://localhost:8080/docs/index.html`.
## Swaggo annotations

| Annotation                          | Description                                             |
| ----------------------------------- | ------------------------------------------------------- |
| `@Summary Create Read Book List`    | A brief summary of what the endpoint does.              |
| `@Description POST method`          | Describes the method used by the endpoint.              |
| `@Accept json`                      | Specifies the input format used by the resource.        |
| `@Produce json`                     | Specifies the output format returned by the resource.   |
| `@Success 201 {string} string "ok"` | Indicates the status code (201) and the message ("ok"). |
| `@Router /book [post]`              | Defines the endpoint's route.                           |
These annotations provide structured details for developers using your API and ensure consistency across documentation.