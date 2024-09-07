#Cheatsheet 
A **channel** is a type of variable in [[Go]] that allows the transfer of information between **Goroutines**.
## Initial implementation:
Here’s a basic example without concurrency:
```go
func main() {
	n := 3
	multiplyByTwo(n)
}

func multiplyByTwo(num int) {
	res := num * 2
	fmt.Println(res)
}
```
### Using a Goroutine:
To execute this function as a Goroutine, we use the `go` keyword before calling the function. Additionally, we introduce `time.Sleep(time.Second)` to wait for the Goroutine to finish:
```go
func main() {
	n := 3
	go multiplyByTwo(n)
    time.Sleep(time.Second)
}

func multiplyByTwo(num int) {
	res := num * 2
	fmt.Println(res)
}
```
In this example, the program is split into two routines:
1. The main routine (function `main`).
2. The Goroutine (function `multiplyByTwo`).
However, this approach has some issues:
- The two parts of the code are **disconnected**. The `main` function has no access to the result of `multiplyByTwo`.
- We don’t know when `multiplyByTwo` completes. This is why we use `time.Sleep()`, which is not optimal.
### Using a channel:
A **channel** allows communication between the two routines. When declaring a channel, you must specify the data type it will carry, and this type cannot change later. You can use any data type, including custom structures.
```go
ch := make(chan int)
```
Now, let’s modify the `multiplyByTwo` function to accept the channel as a second argument:
```go
func multiplyByTwo(num int, ch chan int) {
	res := num * 2
	fmt.Println(res)
}
```
Instead of printing the result directly, we will **write** the result to the channel, allowing communication between the Goroutines:
```go
func multiplyByTwo(num int, ch chan int) {
	res := num * 2
	ch <- res
}
```
### Main Function with channel:
In the `main` function, rather than using `time.Sleep()`, we will **read** the result from the channel. Reading from a channel is a **blocking operation**, meaning the program will wait until the channel receives data.
```go
func main() {
	n := 3
	ch := make(chan int)
	go multiplyByTwo(n, ch)
	fmt.Println(<-ch) // This blocks until data is received from the channel
}
```
1. **Channel Declaration**: `ch := make(chan int)` creates a new channel for `int` values.
2. **Goroutine**: The `multiplyByTwo` function is called as a Goroutine (`go multiplyByTwo(n, ch)`), passing the channel `ch` as an argument.
3. **Blocking Read**: `fmt.Println(<-ch)` waits for the value sent through the channel before continuing execution.
By using channels, we synchronize the Goroutines and make them communicate efficiently without relying on arbitrary sleep functions.