Created: 2024-09-17 17:51
## Family Tree:
1. Computer
2. [[Security]]
-- -
Middleware is an entity that intercepts the lifecycle of a server request or response. Simply put, it’s a piece of code that runs before or after the server handles a request with a response.
In software architecture terms, middleware is a component in our applications that allows us to focus on business logic while handling some low-level complexities.
## Example
To explain what middleware is in detail, let’s start with a simple example that has no practical use.
We have three functions with the same signature: add, subtract, and multiply. Now, let’s assume that for some reason, we need to add behaviors to these three functions. For example, we need to display the time every time one of these functions is invoked.
What should we do? The first thing that comes to mind is modifying all the functions:
```go
func sumar(a, b int) int {
    // Show the date and time
    fmt.Println(time.Now())
    resultado := a + b
    // Do something afterward
    return resultado
}
```
If we follow this logic, we would have to write the same lines of code in every function. What if instead of three functions, we have hundreds of functions? It would be crazy to modify the same logic in hundreds of functions over and over.
## Characteristics
Middleware is:
- A technique used to solve this kind of problem.
- A function that receives another function and returns a new one (with the same signature) but created on the fly with additional functionality.
For example, if we want to add the behavior of displaying the time whenever one of the functions (add, subtract, multiply) is invoked, we can do so by creating the following middleware:
```go
func mostrarTiempo(f func(int, int) int) func(int, int) int {
    return func(a, b int) int {
        fmt.Println(time.Now())
        return f(a, b)
    }
}
```
## Chaining Middlewares
Let’s create another middleware that will show a message after the function is executed:
```go
func mostrarPosterior(f func(int, int) int) func(int, int) int {
    return func(a, b int) int {
        resultado := f(a, b)
        // Do something afterward
        fmt.Println("Function executed")
        return resultado
    }
}
```
Now, we can execute the `sumar` function with the middlewares applied:
```go
func main() {
    fmt.Println("Result: ",
    mostrarTiempo(mostrarPosterior(sumar))(10, 5))
    // It’s the same as doing it step by step:
    // fm1 := mostrarPosterior(sumar)
    // fm2 := mostrarTiempo(fm1)
    // result := fm2(10, 20)
    // fmt.Println(result)
}
```
Each middleware has the power and responsibility to decide whether to execute instructions before, after, or both around the received function.
## Stacking Middlewares:
What happens when stacking middlewares is that each one can process instructions before and after the received function. When the received function is finally executed, it behaves as a single function—accumulating all the functionalities of the previous ones. Let’s see the following code to demonstrate the order in which the instructions of two interceptors are executed:
```go
func main() {
    fmt.Println(inter1(inter2(sumar))(10, 20))
}

func inter1(f func(int, int) int) func(int, int) int {
    return func(a, b int) int {
        fmt.Println("inter1 BEFORE")
        // Execute the received function with the signature func(int, int) int
        resultado := f(a, b)
        fmt.Println("inter1 AFTER")
        return resultado
    }
}
func inter2(f func(int, int) int) func(int, int) int {
    return func(a, b int) int {
        fmt.Println("inter2 BEFORE")
        // Execute the received function with the signature func(int, int) int
        resultado := f(a, b)
        fmt.Println("inter2 AFTER")
        return resultado
    }
}
```
This will show the following result in the console:
```bash
inter1 BEFORE
inter2 BEFORE
inter2 AFTER
inter1 AFTER
```