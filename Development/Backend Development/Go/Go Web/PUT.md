To handle a PUT request in a [[Go]] [[Go Web Server|Web Server]], we need to update an existing product using the provided `ID` in the path parameter. Here's an explanation of how each part works, along with the full implementation:
## Receiving a PUT Request
A PUT request typically updates an existing resource. In this case, the `ID` of the product to be updated is passed in the path parameter `:id`.
### Route Definition:
We define a PUT route in the router:
```go
pr.PUT("/:id", p.Update())
```
### Request Handling:
When a PUT request is received with a specific product ID, the server will attempt to replace the stored product. If the product is not found, it returns an error.
### Repository Implementation:
In the `Repository` interface, we add the `Update` method to update the product:
```go
type Repository interface {
    GetAll() ([]Product, error)
    Store(id int, name, productType string, count int, price float64) (Product, error)
    LastID() (int, error)
    Update(id int, name, productType string, count int, price float64) (Product, error)
}
```
In the implementation, we search for the product by ID, and if found, update its details:
```go
func (r *repository) Update(id int, name, productType string, count int, price float64) (Product, error) {
    p := Product{Name: name, Type: productType, Count: count, Price: price}
    updated := false
    for i := range ps {
        if ps[i].ID == id {
            p.ID = id
            ps[i] = p
            updated = true
        }
    }
    if !updated {
        return Product{}, fmt.Errorf("Product %d not found", id)
    }
    return p, nil
}
```
### Service Layer:
The service calls the repository to update the product:
```go
type Service interface {
    GetAll() ([]Product, error)
    Store(name, productType string, count int, price float64) (Product, error)
    Update(id int, name, productType string, count int, price float64) (Product, error)
```
```go
func (s *service) Update(id int, name, productType string, count int, price float64) (Product, error) {
    return s.repository.Update(id, name, productType, count, price)
}
```
### Handler (Controller) Update method:
The `Update` handler validates the incoming request, checks for required fields, and calls the service layer to update the product. If successful, it returns a 200 response, otherwise an error:
```go
func (c *Product) Update() gin.HandlerFunc {
    return func(ctx *gin.Context) {
        token := ctx.GetHeader("token")
        if token != "123456" {
            ctx.JSON(401, gin.H{ "error": "Invalid token" })
            return
        }

        id, err := strconv.ParseInt(ctx.Param("id"), 10, 64)
        if err != nil {
            ctx.JSON(400, gin.H{ "error": "Invalid ID" })
            return
        }

        var req request
        if err := ctx.ShouldBindJSON(&req); err != nil {
            ctx.JSON(400, gin.H{ "error": err.Error() })
            return
        }

        if req.Name == "" {
            ctx.JSON(400, gin.H{ "error": "Product name is required" })
            return
        }

        if req.Type == "" {
            ctx.JSON(400, gin.H{ "error": "Product type is required" })
            return
        }

        if req.Count == 0 {
            ctx.JSON(400, gin.H{ "error": "Product count is required" })
            return
        }

        if req.Price == 0 {
            ctx.JSON(400, gin.H{ "error": "Product price is required" })
            return
        }

        p, err := c.service.Update(int(id), req.Name, req.Type, req.Count, req.Price)
        if err != nil {
            ctx.JSON(404, gin.H{ "error": err.Error() })
            return
        }

        ctx.JSON(200, p)
    }
}
```
### Main Function:
Finally, in the `main` function, the route for PUT requests is added to handle the update of products:
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

    r.Run()
}
```