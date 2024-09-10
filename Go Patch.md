#Cheatsheet 
How can we receive a PATCH request in a [[Go]] [[Go Web Server|Web Server]]?
```go
   pr.POST("/", p.Store())
   pr.GET("/", p.GetAll())
   pr.PUT("/:id", p.Update())
   pr.PATCH("/:id", p.UpdateName())
```
A PATCH request is received with a path parameter that indicates the ID of the stored product being modified, and only the `name` field is updated.
## Add method in interface
Define a web service using the PATCH method, which will have the path `"products/:id"`. Add the methods to be used in the `Repository` and `Service` interfaces.
```go
type Repository interface {
   GetAll() ([]Product, error)
   Store(id int, name, productType string, count int, price float64) (Product, error)
   LastID() (int, error)
   UpdateName(id int, name string) (Product, error)
   Update(id int,  name, productType string, count int, price float64) (Product, error)
}
type Service interface {
   GetAll() ([]Product, error)
   Store(name, productType string, count int, price float64) (Product, error)
   Update(id int, name, productType string, count int, price float64) (Product, error)
   UpdateName(id int, name string) (Product, error)
}
```
## Repository
The functionality to update the product's name in memory is implemented if it matches the sent ID. Otherwise, an error is returned.
```go
func (r *repository) UpdateName(id int, name string) (Product, error) {
   var p Product
   updated := false
   for i := range ps {
       if ps[i].ID == id {
           ps[i].Name = name
           updated = true
           p = ps[i]
       }
   }
   if !updated {
       return Product{}, fmt.Errorf("Product %d not found", id)
   }
   return p, nil
}
```
## Service
Within the service, the repository is called to proceed with updating the product's name.
```go
func (s *service) UpdateName(id int, name string) (Product, error) {
   return s.repository.UpdateName(id, name)
}
```
## Controller
The `UpdateName` controller is added to the product handler.
```go
func (c *Product) UpdateName() gin.HandlerFunc {
   return func(ctx *gin.Context) {
       token := ctx.GetHeader("token")
       if token != "123456" {
           ctx.JSON(401, gin.H{ "error": "invalid token" })
           return
       }
       id, err := strconv.ParseInt(ctx.Param("id"),10, 64)
       if err != nil {
           ctx.JSON(400, gin.H{ "error":  "invalid ID"})
           return
       }
       var req request
       if err := ctx.ShouldBindJSON(&req); err != nil {
           ctx.JSON(400, gin.H{ "error": err.Error() })
           return
       }
       if req.Name == "" {
           ctx.JSON(400, gin.H{ "error": "Product name is required"})
           return
       }
       p, err := c.service.UpdateName(int(id), req.Name)
       if err != nil {
           ctx.JSON(404, gin.H{ "error": err.Error() })
           return
       }
       ctx.JSON(200, p)
   }
}
```
## Main
In the main program, the router corresponding to the PUT method is added.
```go
func main() {
   repo := products.NewRepository()
   service := products.NewService(repo)
   p := handler.NewProduct(service)
   r := gin.Default()
   pr := r.Group("/products")
   pr.POST("/", p.Store())
   pr.GET("/", p.GetAll())
   pr.PUT("/:id", p.Update())
   pr.PATCH("/:id", p.UpdateName())
   r.Run()
}
```