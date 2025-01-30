Created: 2024-09-17 15:09
## Family Tree:
1. Computer
2. Backend Development
3. [[Go]]
-- -
Basic Go syntax cheatsheet.
## Variables
A variable is a portion of memory storage that temporarily holds data for processing. These are the rules to keep in mind when naming a variable:
- Its name must start with a letter, never with a number.
- Variable names cannot contain spaces.
- If the variable name starts with a lowercase letter, it can only be accessed within the current package. These are considered un-exported variables.
- If the variable name starts with an uppercase letter, it can be accessed from outside the current package. These are considered exported variables.
- If a variable name consists of multiple words, **camelCase** notation is used.
### Syntax:
```go
var name string
```
- **`var`**: A reserved keyword used to declare a variable.
- **`string`**: A data type used to store a string of text. Other types include `int`, `float`, and `bool`.
### Assigning a value to a variable:
We can specify a variable with the `int` data type to declare and use an integer variable:
```go
var hours int
```
We then assign the value "20" to our variable:
```go
hours = 20
```
We can also assign values to multiple variables in a single line:
```go
product, price := "Jeans", 10.5
```
Variable declarations can be grouped into blocks for better readability and code quality:
```go
var (
  product  = "Course"
  quantity = 25
  price    = 40.50
  inStock  = true
)
```
Go also allows assignment without prior declaration. Internally, Go handles the declaration and determines the data type based on the assigned value:
```go
hours := 20
```
## Constants
Constants are values that cannot change during runtime. These are the rules for naming a constant:
- They must follow the same rules as variable names.
- By convention, constant names are usually written in lowercase to easily differentiate them from variables in the source code.
- Constants must be assigned a value at the time of declaration.
- The `:=` syntax cannot be used for constants.
In Go, the reserved word `const` is used to declare them:
```go
const status = "ok"
```
Like variables, constants can also be grouped into blocks for better readability and code quality:
```go
const (
  product  = "Course"
  quantity = 20
  price    = 40.50
)
```
## Data Types
When we talk about data types in Go, we refer to the different ways of representing information. Go has several primitive data types:
### Integers:
- **Signed:** `int` allows us to represent both positive and negative integers.
- **Unsigned:** `uint` allows us to represent non-negative integers only.
We can also specify the bit size for integers. For example, `int8` reserves 8 bits of memory, which allows a range of 255 integers (from -127 to 127). If no size is defined, Go will choose the size based on the processor architecture where the program is compiled.
### Floating-point numbers:
- **`float32`**: Supports decimal numbers with up to 24 digits of precision.
```go
  var floatNumber32 float32
```
- **`float64`**: Supports decimal numbers with up to 53 digits of precision.
```go
  var floatNumber64 float64
```
### Characters or Strings:
Strings represent sequences of text using UTF-8 encoding.
#### Special Characters:
Special characters must be preceded by a backslash:
- `\n`: Newline
- `\"`: Double quote
### Booleans:
A boolean represents a true or false value:
```go
var booleano = true
```
### Byte:
The `byte` type allows us to work directly with bytes:
```go
var myByte byte
```
## Data Collections
### Arrays and Slices:
Both **arrays** and **slices** are data types in Go that allow us to store a homogeneous set of data, meaning data of the same type.
#### Arrays:
To declare an array, we must define a size and a data type. The length of an array is part of its type, meaning the size of the array cannot be changed:
```go
var myArray [2]string
```
To assign a value to an array, specify the position followed by the value:
```go
a[0] = "Hello"
a[1] = "World"
```
To retrieve a value from an array, specify the variable name and the position of the element you want:
```go
fmt.Println(a[0], a[1])
fmt.Println(a)
```
#### Slices:
A slice is declared similarly to an array, but unlike an array, you do not need to specify the size, as Go manages it dynamically. Here's a slice with boolean elements:
```go
var mySlice = []bool{true, false}
fmt.Println(mySlice[0])
```
Slices can also be created using the `make()` function, which generates an array with zero values and returns a slice referencing that array:
```go
a := make([]int, 5) // len(a) = 5
```
##### Slices: Getting a range
You can get a range of values from a slice using two indices separated by a colon. This selects a half-open range, meaning it includes the first element but excludes the last:
```go
primes := []int{2, 3, 5, 7, 11, 13}
fmt.Println(primes[1:4]) // Output: [3 5 7]
```
If you omit a value before or after the colon, it takes all elements up to the start or from the end of the slice.
##### Slices: Length and Capacity
- **Length**: The number of elements in the slice.
- **Capacity**: The number of elements in the underlying array, starting from the first element of the slice.
You can obtain the length and capacity of a slice using the `len()` and `cap()` functions:
```go
fmt.Println(len(mySlice), cap(mySlice))
```
##### Slices: Adding an element
To add elements to a slice, Go provides the `append()` function:
```go
mySlice = append(mySlice, 2, 3, 4)
```
This function takes the slice and the values to be added, and returns a new slice with all previous and new elements.
### Maps:
Maps allow us to create key-value pair variables, defining one data type for the keys and another for the values.
#### Declaring a Map:
There are two ways to instantiate a map:
```go
myMap := map[string]int{}
myMap := make(map[string]string)
```
The `make()` function initializes a map.
#### Maps: Length
To determine how many key-value pairs a map contains, use the `len()` function:
```go
fmt.Println(len(myMap))
```
This returns zero for uninitialized maps.
#### Maps: Accessing elements
To access a map element, call the map name followed by the key in brackets:
```go
var students = map[string]int{"Benjamin": 20, "Nahuel": 26}
fmt.Println(students["Benjamin"])
```
#### Maps: Adding elements
To add an element to a map, use a new key and assign it a value:
```go
students["Brenda"] = 19
```
#### Maps: Updating values
You can update the value of a specific element by referencing its key:
```go
students["Benjamin"] = 22
```
#### Maps: Deleting elements
Go provides the `delete()` function to remove elements from a map:
```go
delete(students, "Benjamin")
```
## Control and Loop Structures
### If Statement:
The `if` statement allows us to control the flow of instructions that our program will follow. This is achieved by evaluating a condition. If the condition is true, a specific portion of code is executed. If the condition is false, the code is not executed.
```go
if condition {
  // Instructions
}
```
#### If / Else:
The `if/else` statement allows us to execute one block of code if the condition is true and a different block if the condition is false.
```go
if condition {
  // Instructions if the condition is true
} else {
  // Instructions if the condition is false
}
```
#### Multiple If / Else Statements:
You can also chain multiple `if/else` statements to evaluate several conditions.
```go
if condition_1 {
  // Instructions
} else if condition_2 {
  // Instructions
} else {
  // Instructions
}
```
#### If with short declaration:
The `if` statement also allows for a compound syntax where a variable can be declared before the condition.
```go
if var declaration; condition {
  // Instructions
}
```
### Switch Statement:
The `switch` statement allows us to evaluate multiple conditional cases and execute instructions based on them. It is an alternative to nested `if/else` statements.
A `switch` is composed of three main parts:
```go
switch expression {
  case condition_1:
    // Instructions
  case condition_n:
    // Instructions
  default:
    // Instructions
}
```
- **`expression`**: The instructions to be executed are based on the value of the expression.
- **`conditions`**: These will be compared to the value of the expression. If a match is found, the corresponding block of instructions is executed.
- **`default`**: This block contains instructions that are executed if none of the conditions are met.
#### Multiple conditions:
Cases can have multiple values separated by commas, indicating that any of those values satisfy the condition:
```go
switch expression {
  case condition_1, condition_2:
    // Instructions
  default:
    // Instructions
}
```
#### Switch with short declaration:
A `switch` statement also allows for the declaration of a variable to be used within the expression:
```go
switch var expression; expression {
  case condition_1:
    // Instructions
  default:
    // Instructions
}
```
#### Switch with fallthrough:
In Go, you can use the `fallthrough` keyword within a case, which forces the execution of the next case block's instructions, even if the next condition doesn't match:
```go
switch expression {
  case condition_1:
    // Instructions
    fallthrough
  case condition_2:
    // Instructions
  default:
    // Instructions
}
```
### For Loop:
The `for` loop allows us to repeatedly execute a block of code. It's commonly used to iterate over a sequence of data (such as slices, arrays, maps, or strings). In Go, `for` is the only loop keyword, and with it, we can create four types of iterations:
1. **Standard for**
2. **While loop**
3. **Range loop**
Additionally, we have two reserved keywords: **`break`** and **`continue`**.
#### Standard For Loop:
This is the most common structure for a `for` loop. It consists of three components:
```go
for i := 0; i < 100; i++ {
  sum += 1
}
```
- **Declaration**: Declares a variable and exposes it within the loop's scope.
- **Condition**: If the condition is true, the code inside the loop executes; if false, the loop ends.
- **Post-declaration**: Typically used to modify the value of the declared variable.
#### While Loop:
The `while` loop allows us to execute a block of code while a condition is true. Unlike the standard `for` loop, it only has one component: the condition. The condition must be updated inside the loop to avoid an infinite loop.
```go
sum := 1
for sum < 10 {
  sum += sum
}
```
#### Range Loop:
The `range` keyword iterates over elements in data structures, always returning two variables:
- **Array or Slice**: The first is the index, and the second is the element.
- **String**: The first is the index, and the second is the rune (character) representation as an `int`.
- **Map**: The first is the key, and the second is the value in the key-value pair.
- **Channel**: The first is the element from the channel, and the second is empty.
Example with an array:
```go
fruits := []string{"apple", "pear"}
for i, fruit := range fruits {
  fmt.Println(i, fruit)
}
```
#### Skip to the next iteration:
The `continue` keyword allows us to skip to the next iteration of a loop before completing all the code in the current iteration. This is useful when certain conditions are met and we want to move on to the next iteration. In the following example, only odd numbers are printed. When the remainder of dividing by 2 is 0 (i.e., the number is even), the loop skips the iteration:
```go
for i := 0; i < 10; i++ {
  if i%2 == 0 {
    continue
  }
  fmt.Println(i)
}
```
#### Breaking a Loop:
The `break` keyword allows us to terminate a loop before it finishes, which is especially useful in infinite loops:
```go
sum := 0
for {
  sum++
  if sum >= 1000 {
    break
  }
}
```
## Functions
In Go, functions are defined using the `func` keyword. Here's a breakdown of the components of a function:
```go
func sum(a int, b int) int {
  sum := a + b
  return sum
}
```
- **`func`**: Reserved keyword indicating the start of a function declaration.
- **`sum`**: The function name. If it starts with a lowercase letter, it will only be accessible within the package where it is defined.
- **`(a int, b int)`**: The parameter list. In this case, the function takes two parameters, `a` and `b`, both of type `int`.
- **`int`**: Return type. If present, the function must include a `return` statement in its body.
### Ellipsis:
Go provides the ellipsis notation (`...`) to allow functions to receive a dynamic number of parameters. This is useful when you don't know the exact number of arguments that will be passed to the function.
For example, here’s a function that uses ellipsis to accept a variable number of `float64` values and returns their sum:
```go
func suma(values ...float64) float64 {
  var resultado float64
  for _, value := range values {
    resultado += value
  }
  return resultado
}
```
- **`values ...float64`**: This allows the function to take a variable number of `float64` arguments.
- **`for _, value := range values`**: Iterates over each `value` in the slice created from the provided arguments, adding them to `resultado`.
### Multiple return values:
One of Go's powerful features is the ability to create functions that return more than one value. To start, you need to specify the data types of the return values, separated by commas and enclosed in parentheses:
```go
func miFuncion(valor1, valor2 float64) (float64, string, int, bool)
```
When calling the function, you can capture all the return values like this:
```go
var1, var2, var3, var4 := miFuncion(valor1, valor2)
```
#### Returning a value and an error:
In Go, multiple returns are often used when you need to return a value along with an error, to check if an operation succeeded or failed. Here's an example of a division function that returns an error if the divisor is zero, using the `errors` package:
```go
import (
  "errors"
)

func division(dividendo, divisor float64) (float64, error) {
  if divisor == 0 {
    return 0, errors.New("El divisor no puede ser 0")
  }
  return dividendo / divisor, nil
}
```
In the `main` function, we validate whether the operation was successful:
```go
func main() {
  res, err := division(2, 0)
  if err != nil {
    // An error occurred
  } else {
    // No error, proceed
  }
}
```
### Named return values:
Go allows you to name return values, defining both the data type and the variable name in the function signature:
```go
func operaciones(valor1, valor2 float64) (suma float64, resta float64, multip float64, divis float64)
```
Inside the function, store the results in the named variables, and then use `return`:
```go
func operaciones(valor1, valor2 float64) (suma float64, resta float64, multip float64, divis float64) {
  suma = valor1 + valor2
  resta = valor1 - valor2
  multip = valor1 * valor2
  divis = valor1 / valor2
  return
}
```
### Returning functions:
You can also create functions that return other functions. To do this, specify the parameters and return types of the function that will be returned:
```go
func miFuncion(valor string) func(valor1, valor2 float64) float64
```
Here’s an example where we pass an operation as a string, and the function returns another function to perform that operation with two numerical values:
```go
func opSuma(valor1, valor2 float64) float64 {
  return valor1 + valor2
}

func opResta(valor1, valor2 float64) float64 {
  return valor1 - valor2
}

func opMultip(valor1, valor2 float64) float64 {
  return valor1 * valor2
}

func opDivis(valor1, valor2 float64) float64 {
  if valor2 == 0 {
    return 0
  }
  return valor1 / valor2
}
```
We can create a function to orchestrate the operation functions:
```go
func operacionAritmetica(operador string) func(valor1, valor2 float64) float64 {
  switch operador {
  case "Suma":
    return opSuma
  case "Resta":
    return opResta
  case "Multip":
    return opMultip
  case "Divis":
    return opDivis
  }
  return nil
}
```
In the `main` function, instantiate the operation function by passing the operation type and perform the operation:
```go
func main() {
  oper := operacionAritmetica("Suma")
  r := oper(2, 5)
  fmt.Println(r)  // Output: 7
}
```