#Cheatsheet 
A **[[Go]] structure** is a typed collection of data fields. For example, we can define a structure "Person" to hold values such as age, weight, gender, profession, etc. Structures are useful for grouping data, allowing the creation of custom records. A structure consists of built-in types and user-defined types (the structure itself is a user-defined type).
## Declaration
Now that we know what a structure is and why it's used, let’s learn how to declare them. In the example below, we see the basic skeleton of a structure:
**`type`** and **`struct`** are keywords, and the structure contains several fields with their defined data types.
```go
type name struct {
  field1 dataType
  field2 dataType
}
```
## Application
We define a structure as follows: Determine its fields, followed by a space and the data type. Fields are separated by line breaks. If the first letter of the structure or its attributes is capitalized, it means they are accessible from other packages.
```go
type Persona struct {
  Nombre    string
  Genero    string
  Edad      int
  Profesion string
}
```
To instantiate a structure, there are different ways:
- Assign values to all fields:
```go
  p1 := Persona{"Celeste", "Mujer", 34, "Ingeniera"}
```
- Assign values to specific fields, leaving the rest to their default values based on their data type:
```go
  p2 := Persona{
  Nombre:    "Nahuel",
  Genero:    "Hombre",
  Edad:      30,
  Profesion: "Ingeniero",
}
```
To access a field of the structure, we proceed as follows:
```go
p2.Edad
```
We can assign or modify a field’s value like this:
```go
p2.Edad = 33
```
You can also define an empty structure and assign values later:
```go
var p3 Persona
p3.Nombre = "Ulises"
p3.Edad = 15
```
## Composition
Structures can be used as data types themselves, meaning that we can have structures as fields within other structures. This is called "composition." For example, we can have a "Preferences" structure inside our "Person" structure. First, we declare our "Preferences" structure:
```go
type Gustos struct {
  Comidas   string
  Peliculas string
  Series    string
  Deportes  string
}
```
Next, we assign a field of type `Gustos` to our `Persona` structure:
```go
type Persona struct {
  Nombre    string
  Genero    string
  Edad      int
  Profesion string
  ListaGustos Gustos
}
```
To access or modify a value from the nested structure:
```go
p2.ListaGustos.Deportes = "fútbol"
```
## Tags
When working with structures in Go, it's possible to define **tags**. Tags are annotations that appear after the data type in a structure declaration. Each tag consists of short strings associated with some corresponding value, and they are enclosed in backticks. Here's an example of how a struct with tags looks:
```go
type MiEstructura struct {
  Campo1 string `miEtiqueta:"valor"`
  Campo2 string `miEtiqueta:"valor"`
  Campo3 string `miEtiqueta:"valor"`
}
```
### Uses cases for tags
For example, when working with REST applications, you can use tags to specify the name of each field in JSON format. The JSON encoder from the standard library uses struct tags as annotations to specify how to name the fields in the resulting JSON output. JSON encoding and decoding mechanisms can be found in the `encoding/json` package.
```go
type Persona struct {
  PrimerNombre string `json:"primer_nombre"`
  Apellido     string `json:"apellido"`
  Telefono     string `json:"telefono"`
  Direccion    string `json:"direccion"`
}
```
#### Omitting empty fields in JSON:
Often, we want to suppress the output of fields that are not set in JSON. Since all Go types have a "zero" value, if we want to omit any fields with their zero value, we must include the `omitempty` attribute in the tag:
```go
type Persona struct {
  PrimerNombre string `json:"primer_nombre"`
  Apellido     string `json:"apellido"`
  Telefono     string `json:"telefono"`
  Direccion    string `json:"direccion,omitempty"`
}
```
#### Ignoring private fields:
Sometimes, certain fields need to be exported from the structures for other packages to interact with them. However, these fields might contain sensitive information, and in such cases, we want the JSON encoder to ignore the field entirely, even if it is set. This is achieved by using the special value `-` as the argument for the JSON struct tag:
```go
type Usuario struct {
  Username string `json:"username"`
  Password string `json:"-"`
}
```