#Cheatsheet 
A **pointer** is a data type whose value is a memory address that refers to or "points to" another variable. One of the advantages of [[Go]] is that it allows us to work with pointers. To create a pointer, we place the `*` operator before the data type we want to store in that memory address.
```go
var p *int
```
In the variable `p`, we have a pointer to a value of type `int`.
## Creating pointers
Pointers can also be created in other ways:
- Using the `new()` function, which takes a data type as an argument.
- Using the variable declaration shorthand `:=`.
```go
var p1 *float64
var p2 = new(float64)
var v float64
p3 := &v
```
## Address operator
To obtain the memory reference or address of a variable, we use the address operator `&` in front of the variable:
```go
var v int = 50
fmt.Println("The memory address of variable v is: ", &v)
```
Here, the variable `v` of type `int` has the value `50` and is stored at a memory address in the format `0x70213332` (example address).
## Dereferencing operator
Dereferencing a pointer means obtaining the value stored at the memory address the pointer references. To do this, we place the `*` operator in front of the pointer variable:
```go
var v int = 50
var p *int
p = &v
fmt.Println("Value of the variable the pointer p points to: ", *p)
```
In this example, the pointer `p` points to the memory address of `v`, and using `*p`, we access the value stored at that address (which is `50`).