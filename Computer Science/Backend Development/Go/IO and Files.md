Created: 2024-09-17 15:02
## Family Tree:
1. Computer
2. Backend Development
3. [[Go]]
-- -
IN/OUT and Files operations in Go.
## OS Package
The `os` package provides various ways to access operating system functionalities.
#### `ReadFile(name string) ([]byte, error)`:
* `ReadFile` reads the named file and returns its contents. A successful call returns `err == nil`. Since `ReadFile` reads the entire file, it doesn't treat an EOF (End of File) from `Read` as an error that needs to be reported.
```go
  content, err := os.ReadFile("folder/file.csv")
```
#### `Create(name string) (*os.File, error)`:
- `Create` creates or truncates the named file. If the file already exists, it is truncated. If the file doesn't exist, it's created with mode `0666` (before applying the umask).
```go
  file, err := os.Create("newFile.txt")
```
If successful, the methods of the returned file can be used for I/O operations.
#### `WriteString(s string) (n int, err error)`:
- `WriteString` writes a string to the specified file.
```go
  _, err := file.WriteString("Added text")
```
#### `Stat() (fs.FileInfo, error)`:
- `Stat` returns a `FileInfo` structure describing the file. If there’s an error, it will be of type `*PathError`.
```go
  info, err := os.Stat("file.txt")
fmt.Println("Is a directory: ", info.IsDir())
fmt.Println("File or directory name: ", info.Name())
fmt.Println("File size in bytes: ", info.Size())
fmt.Println("Last modified date and time: ", info.ModTime())
fmt.Println("File permissions: ", info.Mode())
```
#### `Exit(code int)`:
- `Exit` terminates the current program with the given status code. Conventionally, a code of 0 indicates success, and any non-zero code indicates an error. The program terminates immediately, and deferred functions are not executed. For portability, the status code should be in the range `[0, 125]`.
```go
  os.Exit(0)
```
## I/O Package
The `io` package allows us to perform input and output operations.
#### `Copy(dst io.Writer, src io.Reader) (written int64, err error)`:
- `Copy` copies from `src` to `dst` until EOF is reached on `src` or an error occurs. It returns the number of bytes copied and the first error encountered during the copy, if any.
```go
  t := "Text to copy"
r := strings.NewReader(t)
_, err := io.Copy(os.Stdout, r)
```
#### `ReadAll(r io.Reader) ([]byte, error)`:
- `ReadAll` reads from `r` until an error or EOF is reached and returns the data read as a byte slice.
```go
t := "Text to read"
r := strings.NewReader(t)
b, err := io.ReadAll(r)
```
#### `WriteString(w io.Writer, s string) (n int, err error)`:
- `WriteString` writes the string `s` to `w`, which accepts a slice of bytes.
```go
  t := "Text to write"
_, err := io.WriteString(os.Stdout, t)
```