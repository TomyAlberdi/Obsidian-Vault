Created: 2024-09-17 14:57
## Family Tree:
1. Computer
2. [[Backend Development]]
-- -
Go is a language recently launched by Google — in 2009 — and was designed by Robert Griesemer, Rob Pike, and Ken Thompson.
Since it’s a new language, it was natively designed to provide simple solutions to most of the common problems faced by software engineers:
- It fully leverages the use of multiple processors, making it attractive for high-performance systems by saving processing power, particularly in cloud-based systems.
- The code is easy to maintain, which ensures stability.
- It has a high compilation speed. While many applications rely on the Spring framework (and thus require some time to respond to HTTP requests upon startup), Go services take less time to start because they use the available implementations from the standard library.
- It offers autonomous code optimization.
- It natively includes the capability to develop APIs without requiring numerous external libraries, making it simple, easy, and robust.
- It combines the ease of programming found in interpreted and dynamic languages with the efficiency and security of a compiled language.
As a result, it's no surprise that — up to now — Go has been primarily used in businesses and server environments, where the stability and performance of services play a particularly important role. It is especially in container-based virtualization where there is a significant demand for this young programming language. So, it should come as no surprise that Docker, the most prominent representative in container platforms, is based on Go.
## Go code organization
### Packages:
Go applications are organized in packages. A package is a collection of source files located in the same directory. All source files in a directory must share the same package name. When a package is imported, only entities (functions, types, variables, constants) whose names start with a capital letter can be used / accessed. The recommended style of naming in Go is that identifiers will be named using `camelCase`, except for those meant to be accessible across packages which should be `PascalCase`.
So, to declare one of these files, we use the following syntax:
```go
package packagename
```
The folder containing the various files of the package and the package itself must have the same name. The package declaration must be the first line of code in the Go source file.
All functions, types, and variables defined in the Go source file become part of the declared package. The package name should be a single word written entirely in lowercase.
Go programs begin execution in the `main` package. This is a special package used for programs intended to be executables. These are known as commands. Other programs are simply referred to as packages.
#### Importing Packages:
Go provides us with two ways to import packages.
- **Single Package import**:
```go
  import "fmt"
  import "time"
```
- **Grouped Package import**:
```go
  import (
	  "fmt"
	  "time"
  )
```
##### Package fmt:
When calling a function from the `fmt` package, Go automatically imports the package to be used.
- **`fmt.Println()`**: This function allows us to print to the console whatever is passed as a parameter, and it also inserts a newline.
- **`fmt.Printf()`**: Similar to the previous function, but with the difference that it allows the use of conversion characters. For example, `%s` (string) or `%d` (integers).
- **`fmt.Sprintf()`**: Works the same way as `fmt.Printf()`, but instead of displaying output on the screen, it generates a string.
- **`fmt.Scan()`**: Reads text from the standard input (stdin) until it encounters the first space or newline.
- **`fmt.Scanf()`**: Similar to `fmt.Scan()`, but it is used to store multiple arguments separated by spaces.
#### Main Function:
The `main()` function is special because it is the entry point of an executable program. Here’s an example of an executable Go program:
```go
package main
func main() {
  // Code
}
```
### Modules:
Before starting a Go module, we must ensure that a new repository is created on GitHub — or other version control sites like GitLab. Then, we can clone the repository. To initiate a Go module, we use the following command: 
`go mod init github.com/GitHubUser/go-simple-module`
The domain and module name must match the name of the repository that was previously created.
Once the module is initiated, a `.go.mod` file is created. This file contains the dependencies used in the application.
#### Adding a Dependency:
You can add a dependency to the application using the `go get` command. Go allows the use of the `-u` flag to download the dependency if it doesn't exist or to update it:
`go get -u github.com/gin-gonic/gin`
After adding the dependency, it can be used in our module files by adding the import statement:
```go
import (
  "fmt"
  "github.com/gin-gonic/gin"
)
```