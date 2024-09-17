Created: 2024-09-17 15:05
## Family Tree:
1. Computer
2. Backend Development
3. [[Go]]
-- -
In simple terms, a **panic** is an abrupt interruption in the execution of a Go program, indicating that something went wrong unexpectedly. Certain operations in Go can trigger a panic automatically, stopping the program. These situations usually arise from programmer errors that the compiler doesn’t catch.
Some common operations that cause a panic include:
- Exceeding the array index capacity.
- Invoking methods on `nil` pointers.
- Trying to use closed channels.
These types of errors are typically due to mistakes made during development.
## Creating a Panic
In addition to operations that cause a panic by default, you can also manually trigger and customize your own panic using the built-in `panic()` function. A common use case for this is aborting the program when an error occurs that you either don’t want to handle or don’t know how to handle yet.
#### Example:
Let's look at an example where we use the `panic()` function. First, ensure that your package is defined as `main` and import the necessary `fmt` and `os` packages.
```go
package main

import (
  "fmt"
  "os"
)

func main() {
  fmt.Println("Starting...")
  _, err := os.Open("no-file.txt")
  if err != nil {
    panic(err)  // Triggers a panic if the file is not found
  }
  fmt.Println("End")
}
```
When you run this program, you'll get an output similar to this:
![[image.png]]
- The program encounters a panic because the file `no-file.txt` does not exist.
- The panic message is printed, showing the error returned by `os.Open`, which is that the file wasn’t found.
- A **stack trace** is printed, indicating the exact location in the code where the panic occurred.
- The program terminates abruptly with an **exit status 2**. The line `End` is never printed because the execution stopped at the panic.
### Index out of bounds panic:
This case occurs when we try to access an index beyond the length of a slice or the capacity of an array. In this case, Go will produce a runtime panic. Let’s define our `main` package and import the `fmt` package to see an example:
```go
func main() {
   animals := []string{
       "cow",
       "dog",
       "hawk",
   }
   fmt.Println("only the flies: ", animals[len(animals)])
}
```
When running our program, we’ll get a console output similar to this:
![[image 1.png]]
Upon checking the console output, we see that:
- A panic occurred when attempting to access an index that exceeds the length of the created slice.
- Go terminated at runtime.
- The instructions after the panic were not executed. This happens because when a panic occurs, it calls the deferred functions from the panicking function and aborts the program.
### Null receivers:
Go allows us to work with pointers to reference a specific instance of an existing type in the memory at runtime. Pointers can take the `nil` value to indicate that they don’t point to anything. When we attempt to invoke methods on a pointer that has a `nil` value, a panic will occur.
#### Example:
```go
type Dog struct {
   Name string
}

func (s *Dog) WoofWoof() {
   fmt.Println(s.Name, " goes woof woof")
}

func main() {
   s := &Dog{"Sammy"}
   s = nil
   s.WoofWoof()
}
```
When running our program, we’ll get a console output similar to this:
![[image 2.png]]
Upon checking the console output, we see that:
- A panic occurred when attempting to access an invalid memory address or dereference a null receiver.
- The panic occurred at runtime and aborted the program with status 2.
## Defer / Recover
So, what can we do to control the effects of a panic? With the built-in `defer` and `recover` statements, we can control the effects of a panic and prevent our program from terminating in an undesirable way.
`defer` and `recover` are built-in functions in the language, specifically designed to avoid or control the destructive nature of a panic. While they are presented as independent functions, they need to be used together to achieve the best performance results.
### Defer:
`Defer` is a built-in statement in Go that allows us to delay the execution of certain functions and ensure they are executed before the program terminates. It can be said that it’s similar to `ensure` or `finally` used in other programming languages.
It is useful to ensure resources are cleaned up during the execution of our program, even before a panic occurs. It is used as a safety measure to protect against execution cuts and abrupt exits caused by panics.
Functions are deferred by invoking them as usual and prefixing the entire instruction with the keyword `defer`.
#### Example:
```go
func main() {
  // apply "defer" to the invocation of an anonymous function
  defer func() {
    fmt.Println("This function runs despite the panic")
  }()
  // create a panic with a message indicating it occurred
  panic("panic occurred!")
}
```
When running our program, we’ll get a console output similar to this:
![[image 3.png]]
Upon checking the console output, we see that:
- The deferred anonymous function was executed and printed its message.
- The panic that was generated in our `main` function was detected.
- The program exited with status 2.
#### Keep in mind:
- While deferred functions are executed even when panics occur, they are not executed when the function `log.Fatal()` is called.
- If multiple functions were deferred, they are called in reverse order, starting with the last deferred function and ending with the first.
### Recover:
`Recover` is a built-in function that allows us to intercept a panic and prevent it from terminating the program unexpectedly or undesirably.
As part of Go’s built-in package, it can be invoked without importing additional packages.
The correct way to use the `recover` function is inside a `defer` statement. This way, when a panic occurs, the deferred function will recover the panicking routine and the value set in panic, preventing the program from ending unexpectedly.
If `recover` is used outside of a `defer` statement, the panic will terminate the program before `recover` can retrieve the panic value. In this case, `recover` would return `nil` and would not prevent the abrupt end of execution.
#### Example:
Let’s define our `main` package, import the `fmt` package, and try an example of `recover`.
We will declare a function called `isPair()` that takes an integer as an argument and checks if it is even. If the number is odd, it will trigger a panic and call the deferred anonymous function that contains the `recover` function. The panic will be controlled, and its value recovered by `recover` will be assigned to the `err` variable. Since `err` is not `nil`, the recovered value from the panic will be printed to the console, the deferred function will finish executing, and the program will continue.
```go
func isPair(num int) {
  defer func() {
    err := recover()
    if err != nil {
      fmt.Println(err)
    }
  }()
  if (num % 2) != 0 {
    panic("not an even number")
  }
  fmt.Println(num, " is an even number")
}
```
In our `main` function, we will call the `isPair()` function and pass an odd number as an argument to generate a panic. We will see that the panic generated in the function is controlled by `recover` and does not abort the execution of our `main` function.
```go
func main() {
  num := 3
  isPair(num)
  fmt.Println("Execution completed!")
}
```
When running our program, we’ll get a console output similar to the following. Note how the panic value was recovered by `recover`, and the program completed its execution to the end.
```go
not an even number
Execution completed!
```