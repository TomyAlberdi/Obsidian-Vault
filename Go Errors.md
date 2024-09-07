#Cheatsheet 
In [[Go]], an error is an [[Interfaces|interface]] type, built-in like any other. Therefore, no rigid or special control structures are required for error handling.
An error value function represents any value that can describe itself as a string. This is the declaration of the `error` interface:
```go
type error interface {
  Error() string
}
```
Thus, `error` is an interface type whose `Error()` method returns a string.
### Example:
A typical implementation of the `Error()` method from the built-in `error` interface is as follows:
```go
func (e *MyError) Error() string {
  return "My error info"
}
```
## Differences from other languages
Unlike other languages like Java, C#, and JavaScript, Go allows handling errors as any other type of data in the language. No special or rigid structures are required. In other words, errors are treated just like any other task that isn’t exclusively related to error handling.
## Customizing Errors
Go provides a few main functions for creating and customizing our errors:
- `Error()`
- `errors.New()`
- `fmt.Errorf()`
These three alternatives are quite similar. However, we'll focus on the `errors` library, as it is the most commonly used by the community.
### `errors.New()`:
The `New()` function from the `errors` package allows us to create a new basic error with a given message (string).
`errors.New("string")` takes a single argument: an error message of type string that we can customize to inform what caused the error.
#### Example:
We define our `main` package and import the `fmt` and `errors` packages.
```go
package main 
import (
  "fmt"
  "errors"
)

func main() {
  statusCode := 404
  if statusCode > 399 {
    fmt.Println(errors.New("The request has failed"))
    return
  }
  fmt.Println("The program finished successfully")
}
```
In this example, we declare our `main()` function and define a variable called `statusCode` with an `int` value. Then, we perform a validation to check if `statusCode` is greater than 399. If it is, we use `errors.New()` to generate an error message.
## Error Chains
In Go, you can wrap one error inside another, forming a hierarchy of errors, where an instance of an error wraps another, and this one can wrap yet another. Essentially, errors in Go form **error chains**. To wrap an error inside another, we use the `fmt.Errorf()` function with the `%w` directive.
```go
error_1 := fmt.Errorf("First error")
error_2 := fmt.Errorf("Second error: %w", error_1)
```
## `errors` package
As mentioned earlier, Go provides a native package called `errors` to handle errors in our programs. It contains four main functions:
- `New()`
- `Unwrap()`
- `As()`
- `Is()`
Let’s take a closer look at each of them:
### `New()`:
This is the simplest function. As we discussed before, it takes a string argument and returns it as a variable of type `error`:
```go
err := errors.New("new error")
```
### `Unwrap()`:
This function allows us to **unwrap** errors inside a chain. It takes the last error in the chain and checks if it contains another error. If it does, it returns that error; otherwise, it returns `nil`.
Here’s an example where we create `error_1` and then `error_2` by wrapping the first one. We call `Unwrap()` and pass `error_2` as an argument. It returns the error it wraps.
If we compare the unwrapped error (`err`) with `error_1`, we’ll see they are equal.
```go
error_1 := fmt.Errorf("First error")
error_2 := fmt.Errorf("Second error: %w", error_1)
err := errors.Unwrap(error_2)
if err == error_1 {
  fmt.Println("same error")
}
```
### `As()`:
The `As()` function takes two arguments: an `err` (of type `error`) and a `target` (an empty interface). It allows passing a pointer to an error type and returns a boolean.
What this function does is it compares—within the error chain of `err`—the error type with the target pointer. When it finds a match, it assigns the error to the target and returns `true`.
Here’s an example where we attempt to open a non-existent file using `Open()`, which generates an error assigned to `err`. We then define a variable of type pointer to `PathError`, which indicates what went wrong with the file operation. We use the `As()` function to perform the type comparison, and if it finds a match, it returns `true`.
```go
_, err := os.Open("non_existent_file.txt")
var pathErr *os.PathError
if errors.As(err, &pathErr) {
  fmt.Println("Error related to file operation")
}
```
### `Is()`:
The `Is()` function takes two arguments of type `error`, `err` and `target`. It checks the error chain of `err` to see if it matches the `target` error and returns `true` if a match is found.
This function is used when we need to determine if a specific error occurred within the error chain. It compares error-to-error directly.
In the following example, we attempt to open a non-existent file using the `Open()` function, generating an error assigned to `err`. We then define an error variable (`notExist`) that is equal to `fs.ErrNotExist`, indicating that the file does not exist. We use the `Is()` function to compare the error types, and if a match is found, it returns `true`.
```go
_, err := os.Open("not_exist.txt")
var notExist error = fs.ErrNotExist
if errors.Is(err, notExist) {
  fmt.Println("The file does not exist")
}
```
## Returning Errors:
In Go, **multi-return functions** play a crucial role in error handling. Go allows functions to return multiple values, and one of these can be an error. This approach provides a clean way to signal errors without using exceptions, as is common in other languages. Interfaces allow us to implement the same behavior across different objects, and Go’s built-in error handling leverages this feature by often returning an `error` type as one of the multiple return values.
### Syntax:
To create a function that returns more than one value (including an error), you list the types of each returned value in parentheses in the function signature. The `error` value indicates a failure condition in the function, signaling that something went wrong during execution.
The idiomatic Go convention is that the **error is always the last value returned** by the function.
#### Example:
Here is a function `sayHi()` that returns a greeting message (a string) and an error. The error occurs when the `name` argument is empty:
```go
func sayHi(name string) (string, error) {
  if name == "" {
    return "", errors.New("No name provided")
  }
  return fmt.Sprintf("Hi, %s", name), nil
}
```
When calling this function, we must handle the two returned values according to the function’s signature.
```go
greeting, err := sayHi(name)
```
### Null Value:
In Go, when returning an error from a multi-return function, the **non-error values** should be set to their **zero value** (the default value for their type). This ensures that even in error conditions, all return values are properly defined.
#### Zero Values for Common Types:
- **int, float**: `0`
- **string**: `""`
- **bool**: `false`
- **interface, error**: `nil`
In the previous example, if an error occurs (when `name` is an empty string), the function returns the zero value for the string and an error:
```go
if name == "" {
  return "", errors.New("No name provided")
}
```
### Discarding unwanted return values
Sometimes, you're only interested in the error and want to ignore the other return values. In Go, you can discard unwanted values by using the **blank identifier** (`_`).
```go
_, err := sayHi(name)
```
### Validations:
When a function returns an error alongside other values, it’s important to check if the error is `nil` (i.e., no error occurred) before proceeding with the code. This pattern is essential to error handling in Go.
#### Example:
```go
greeting, err := sayHi(name)
if err != nil {
  fmt.Println("Error: ", err)
  return
}
fmt.Println(greeting)
```
The statement `if err != nil` is the standard way to handle errors in Go. If an error occurs, the program flow is altered to handle the error (typically by returning or logging the error). If no error occurs (`err == nil`), the function proceeds normally, which is often referred to as the **happy path**.