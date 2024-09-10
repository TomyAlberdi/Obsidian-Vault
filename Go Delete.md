#Cheatsheet 
How can we receive a DELETE request in a [[Go]] [[Go Web Server|Web Server]]?
```go
   pr.POST("/", p.Store())
   pr.GET("/", p.GetAll())
   pr.PUT("/:id", p.Update())
   pr.PATCH("/:id", p.UpdateName())
   pr.DELETE("/:id", p.Delete())
```
A DELETE request is received with a path parameter that indicates the ID of the stored product to be deleted.
**Request:** 
- No data is needed in the body. 
- Only the product ID to be deleted needs to be specified in the route parameter for correct identification.
**Response:** 
- If the server finds the specified ID while processing the request, the product is deleted, and a 2xx status is returned.
- The response body can contain an updated list of the products to verify that the specified one was deleted.
## Add method in interface
A web service is defined using the DELETE method, with the path `"products/:id"`. Add the methods to be used in the `Repository` and `Service` interfaces.
```go
type Repository interface {
   GetAll() ([]Product, error)
   Store(id int, name, productType string, count int, price float64) (Product, error)
   LastID() (int, error)
   UpdateName(id int, name string) (Product, error)
   Update(id int,  name, productType string, count int, price float64) (Product, error)
   Delete(id int) error
}
type Service interface {
   GetAll() ([]Product, error)
   Store(name, productType string, count int, price float64) (Product, error)
   Update(id int, name, productType string, count int, price float64) (Product, error)
   UpdateName(id int, name string) (Product, error)
   Delete(id int) error
}
```
## Repository
The functionality to delete the product in memory is implemented if it matches the sent ID. Otherwise, an error is returned.
```go
func (r *repository) Delete(id int) error {
   deleted := false
   var index int
   for i := range ps {
       if ps[i].ID == id {
           index = i
           deleted = true
       }
   }
   if !deleted {
       return fmt.Errorf("Product %d not found", id)
   }
   ps = append(ps[:index], ps[index+1:]...)
   return nil
}
```
## Service
Within the service, the repository is called to proceed with deleting the product.
```go
func (s *service) Delete(id int) error {
   return s.repository.Delete(id)
}
```
## Controller
The `Delete` controller is added to the product handler.
```go
func (c *Product) Delete() gin.HandlerFunc {
   return func(ctx *gin.Context) {
       token := ctx.GetHeader("token")
       if token != "123456" {
           ctx.JSON(401, gin.H{ "error": "invalid token" })
           return
       }
       id, err := strconv.ParseInt(ctx.Param("id"), 10, 64)
       if err != nil {
           ctx.JSON(400, gin.H{ "error": "invalid ID" })
           return
       }
       err = c.service.Delete(int(id))
       if err != nil {
           ctx.JSON(404, gin.H{ "error": err.Error() })
           return
       }
       ctx.JSON(200, gin.H{ "data": fmt.Sprintf("Product %d has been deleted", id) })
   }
}
```
## Main
In the main program, the router corresponding to the DELETE method is added.
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
   pr.DELETE("/:id", p.Delete())
   r.Run()
}
```