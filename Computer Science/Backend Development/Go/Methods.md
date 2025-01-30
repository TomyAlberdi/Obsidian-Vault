Created: 2024-09-17 15:03
## Family Tree:
1. Computer
2. Backend Development
3. [[Go]]
-- -
A **method** in Go is a function with a special receiver argument. The receiver appears in its own list of arguments between the `func` keyword and the method name. In Go, methods can be defined for types, including user-defined types such as structures.
## Declaration
To declare methods, you need a structure (Structures). For example, let’s declare a `Circle` structure that will store the radius:
```go
type Circulo struct {
  radio float64
}
```
In Go, defining a method for a structure is similar to declaring a function, but with some key differences:
```go
func (v miEstructura) metodo() { }
```
In this syntax:
- **`v`** is the variable used to manipulate the structure within the method.
- **`miEstructura`** is the structure that the method is associated with.
## Adding Logic
Let's define our first method for the `Circulo` structure. The variable `c`, which belongs to the `Circulo` structure, will allow us to access the structure's fields. Here’s a method to calculate the area of a circle:
```go
func (c Circulo) area() float64 {
  return math.Pi * c.radio * c.radio
}
```
In this method:
- The receiver `c` is of type `Circulo`, which allows access to its `radio` field.
- The method `area()` calculates and returns the area of the circle using the formula πr^2
## Composition
In other languages, there is the concept of **Inheritance**, which involves having a parent class and child classes. The parent class passes its code to the child classes. Go doesn't have the concept of inheritance, but it provides **composition (Structures > Composition)**, where the parent structure is used as a field within child structures. This is known as **embedding structs**.
The purpose of composition in Go is to allow building larger programs from smaller components. It helps in designing various data types and implementing different behaviors on them.
### Example:
We declare our parent class `Vehicle`, and add the fields `km` (kilometers) and `time`:
```go
type Vehiculo struct {
  km     float64
  tiempo float64
}
```
We also declare a method for our `Vehicle` class that prints the value of its fields:
```go
func (v Vehiculo) detalle() {
  fmt.Println("km: ", v.km)
  fmt.Println("tiempo: ", v.tiempo)
}
```
Next, we declare the `Auto` structure. In it, we add a field of type `Vehiculo`, embedding the structure:
```go
type Auto struct {
  v Vehiculo
}
```
We add a method that takes time in minutes and calculates the distance based on a speed of 100 km/h:
```go
func (a *Auto) Avanzar(minutos int) {
  a.v.tiempo = float64(minutos) / 60
  a.v.km = a.v.tiempo * 100
}
```
Now, the `Detalle` method calls the method from the parent class:
```go
func (a *Auto) Detalle() {
  fmt.Println("Vehículo: Auto")
  a.v.detalle()
}
```
Finally, we execute our method in the `main` function and see the results:
```go
func main() {
  auto := Auto{}
  auto.Avanzar(360)
  auto.Detalle()
}
```