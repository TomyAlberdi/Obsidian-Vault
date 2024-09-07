#Cheatsheet 
An **[[Interfaces|interface]]** in [[Go]] defines a set of methods that must be implemented, without specifying how those methods are defined. Interfaces provide modularity in the language, allowing multiple types to share common behavior without needing to modify existing code.
### Example 1:
We create a `circle` structure and define functions to calculate and display the area and perimeter of the circle:
```go
type circle struct {
  radius float64
}

func (c circle) area() float64 {
  return math.Pi * c.radius * c.radius
}

func (c circle) perim() float64 {
  return 2 * math.Pi * c.radius
}
```
Now, we create a `details` function to print the area and perimeter of the circle:
```go
func details(c circle) {
  fmt.Println(c)
  fmt.Println(c.area())
  fmt.Println(c.perim())
}
```
#### Problem:
What if we want to handle other geometric shapes using the `details` function? This is where **interfaces** come into play. Interfaces allow us to implement the same behavior for different objects.
### Example 2:
We define an interface `geometry` that contains two methods: `area()` and `perim()`. Any object implementing these methods can be passed to the `details` function:
```go
type geometry interface {
  area() float64
  perim() float64
}
```
Now, we create another geometric shape, a `rectangle`, which has the same methods:
```go
type rectangle struct {
  width, height float64
}

func (r rectangle) area() float64 {
  return r.width * r.height
}

func (r rectangle) perim() float64 {
  return 2*r.width + 2*r.height
}
```
We modify the `details` function to accept any geometric shape that implements the `geometry` interface:
```go
func details(g geometry) {
  fmt.Println(g)
  fmt.Println(g.area())
  fmt.Println(g.perim())
}
```
Now, the `details` function can be used for multiple geometric shapes without modification.
### Reusing the function
To make our function reusable for different geometric shapes, we can create a function `newGeometry` that returns an interface, capable of implementing any of our geometric objects.
We define a function that receives a type and the dimensions required to create the object:
```go
const (
  rectType   = "RECT"
  circleType = "CIRCLE"
)

func newGeometry(geoType string, values ...float64) geometry {
  switch geoType {
  case rectType:
    return rectangle{width: values[0], height: values[1]}
  case circleType:
    return circle{radius: values[0]}
  }
  return nil
}
```
#### Implementing in Main:
We can now create different geometric objects and print their details:
```go
func main() {
  r := newGeometry(rectType, 2, 3)
  details(r)

  c := newGeometry(circleType, 4)
  details(c)
}
```
### Conclusion:
By using interfaces, we can handle multiple types of geometric shapes with the same function, making our code more modular and reusable.
## Empty Interfaces
An **empty interface** is an interface that has no methods declared. The utility of these interfaces is to provide a "wildcard" data type, allowing us to store values of unknown or varying data types, depending on the program's flow.
```go
var miVariable interface{}
```
As mentioned earlier, an interface defines the minimal set of methods that a data type must implement to be considered an implementer of that interface. Since an empty interface defines zero methods, **all data types** are considered implementers of the empty interface because they implement "at least" zero methods.
### Example:
```go
type ListaHeterogenea struct {
  Data []interface{}
}

func main() {
  l := ListaHeterogenea{}
  l.Data = append(l.Data, 1)
  l.Data = append(l.Data, "string")
  l.Data = append(l.Data, true)
}
```
In this example:
- The `ListaHeterogenea` struct has a field `Data` that is a slice of `interface{}`, meaning it can store values of any type.
- In the `main` function, we append an integer (`1`), a string (`"string"`), and a boolean (`true`) to the `Data` field.
This demonstrates the flexibility of the empty interface, as it can hold values of different types within the same slice.
## Type Assertion
Type assertion provides access to the exact data type that is abstracted by an interface.
```go
var i interface{} = "hello" // 'i' is an interface holding a string value
s := i.(string) // Assert that 'i' holds a string, assigning it to 's'
fmt.Println(s)  // Prints: hello

s, ok := i.(string)  // Assert again, with a boolean check
fmt.Println(s, ok)   // Prints: hello true

f, ok := i.(float64) // Try asserting 'i' as a float64, with a boolean check
fmt.Println(f, ok)   // Prints: 0 false (because 'i' is not a float64)

f = i.(float64)      // This will cause a panic because 'i' does not hold a float64
fmt.Println(f)
```
This code demonstrates how type assertion works in Go, allowing you to retrieve the actual type from an interface and handle potential mismatches gracefully using a comma-ok idiom.