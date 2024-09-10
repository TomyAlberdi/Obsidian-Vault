#Development 
[[Go]] applications use contexts to control and manage crucial aspects of applications, such as cancellation and data sharing in [[Go Concurrency and Parallelism|concurrent programming]].
**Web Context** is a package of information that is sent between the different layers of our application. It is generally created when a new request arrives at the API. This package will be transmitted to the service layer and the storage layer.
The context package begins with some important functionality:
- The ability to store additional information that can be transmitted throughout the propagation.
- The ability to control cancellation. You can create packages that stop the execution of your code if they exceed a specific deadline or a timeout value.
## Context with value
One of the most common uses of `context` is to share data or use request-scoped values. When we have several functions and want to share data between them, we can do this using contexts. The easiest way to do this is by using the `context.WithValue` function. This creates a new context based on a parent context and adds a value to a given key.
We can think of the context as a map, so we can add and retrieve values by key. This is very useful as it allows us to store any type of data within the context.
```go
ctx := context.Background()
context.WithValue(ctx, "api-key", "secret-api-key")
```
It is important to note that the `WithValue()` function returns a copy of the existing context and does not modify the original context.  
With the `Value("key")` function, we can read the value of the key we request. Keep in mind that when we try to access a key-value pair in a context that does not exist, it will return `nil`.
```go
apiKey := ctx.Value("api-key")
```
## Context cancellation
Another very useful feature of context in Go is the ability to cancel related processes. It is good practice to propagate the cancellation signal when received.  
Let's say we have a function where dozens of goroutines are initiated. That main function waits for all the routines to finish or for a cancellation signal before continuing.
To create a context with cancellation, we just need to call the `context.WithCancel()` function, passing its context as a parameter. This will return a new context and a cancellation function. To cancel that context, we just need to call the cancellation function.
```go
ctx, cancel := context.WithCancel(context.Background())
defer cancel()
```