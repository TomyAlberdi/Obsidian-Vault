Created: 2024-09-17 14:59
## Family Tree:
1. Computer
2. Backend Development
3. [[Go]]
-- -
We've seen applications that execute sequentially, meaning that one line of code doesn't run until the previous one finishes. However, Go has a feature called **concurrency**, which allows different lines of code to execute simultaneously.
Concurrency in Go is the ability to separate the execution of multiple tasks individually, without them blocking each other. To achieve this, Go provides **Goroutines**, which can be considered lightweight threads of execution, as the cost of creating Goroutines is much smaller compared to creating an OS thread.
## Concurrency vs Parallelism
It's important to distinguish between concurrency and parallelism. The main difference is that concurrency is about the coordination or synchronization of multiple tasks at once, while parallelism actually executes tasks simultaneously.
In other words, concurrency structures programs in a way that two or more tasks can make progress at the same time, whereas parallelism allows two or more tasks to **run** at the same time.
## Goroutines
As mentioned earlier, Goroutines are lightweight threads managed by Go at runtime. While traditional threads are limited by the number of available cores and are managed by the operating system, multiple Goroutines can run within the same thread and are efficiently managed by Go’s runtime.
To create a Goroutine, we add the keyword **`go`** before a function call, and Go's runtime will not block the code execution. Instead, it runs the function in the background while the main thread continues its execution.
#### Example:
If we run the following example, we'll encounter a problem:
```go
func greet(names []string) {
	for _, name := range names {
		fmt.Printf("Hello %s\n", name)
	}
}

func sayGoodbye(names []string) {
	for _, name := range names {
		fmt.Printf("Goodbye %s\n", name)
	}
}

func main() {
	names := []string{"Orlando", "Daniela", "Andrea"}
	go greet(names)
	go sayGoodbye(names)
}
```
The program terminates without printing anything to the console. This is because the `main` function finishes before `greet` and `sayGoodbye` have a chance to execute.
#### Solutions:
There are several ways to solve this issue:
- Use `time.Sleep()` in the `main` function to delay its termination.
- Use `fmt.Scan()` at the end of `main` to wait for user input before terminating.
- Have the Goroutines communicate with each other to notify when they have finished their tasks.
For the latter, Go provides a special data type called **channel**, which acts as a communication portal between different Goroutines.
### Advantages of Goroutines:
- They are **cheaper** than traditional threads.
- The number of Goroutines can grow or shrink according to the program’s requirements.
- Goroutines can communicate with each other using a channel, specially designed to prevent race conditions and avoid shared memory overuse.
### Golden rules of Goroutines:
- Know **how and when** a Goroutine will finish. If possible, it's preferable to wait for all the Goroutines created in a function to finish before exiting.
- Manage the lifecycle of a Goroutine in a **final block**.