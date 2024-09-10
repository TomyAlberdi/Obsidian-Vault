In [[Go]], the `func Marshal(v interface{}) ([]byte, error)` function takes a value of any type as a parameter and returns a byte slice containing its JSON representation. It also returns an error if something goes wrong during the process.
When using `json.Marshal()` and passing a struct as a parameter, the fields that will be converted to JSON must be **exported** (i.e., capitalized). This is because un-exported fields (lowercase) are not accessible outside the package and cannot be marshaled into JSON.
Here’s an example where we define a struct called `product` with the fields `Name`, `Price`, and `Published` of various types. All fields are capitalized to be exported and eligible for conversion to JSON using the `Marshal()` function.
After calling the `Marshal()` function, it returns the result as a `[]byte`. We check for errors and then print the result as a string, since it's returned as a byte slice.
#### Example:
```go
type product struct {
  Name      string
  Price     int
  Published bool
}

p := product{"MacBook Pro", 1500, true} // Create a product instance.
jsonData, err := json.Marshal(p)        // Convert the struct to JSON.
if err != nil {
  log.Fatal(err)                        // Handle the error if something goes wrong.
}
fmt.Println(string(jsonData))            // Convert the byte slice to a string and print it.
```
Output:
```bash
{"Name":"MacBook Pro","Price":1500,"Published":true}
```
## `Unmarshall` function
The `func Unmarshal(data []byte, v interface{}) error` function takes a byte array as its first parameter and a pointer to a struct as its second parameter. If the byte array contains valid JSON data, the function decodes it and populates the struct with the corresponding data. It returns an error if it encounters any issues.
Here, we define a JSON string `jsonData`, which contains a valid JSON object that matches the structure of our previously defined `product` struct. Next, we create an empty `product` struct called `p`, and pass it to the `Unmarshal` function along with our JSON string (converted to a byte slice). Finally, we print the struct after it has been populated with the data from the JSON.
#### Example:
```go
type product struct {
  Name      string
  Price     int
  Published bool
}

jsonData := `{"Name":"MacBook Air", "Price":900, "Published":true}` // JSON string.
var p product                              // Create an empty product struct.
if err := json.Unmarshal([]byte(jsonData), &p); err != nil {  // Unmarshal the JSON into the struct.
  log.Fatal(err)                          // Handle the error if something goes wrong.
}
fmt.Println(p)                             // Print the populated struct.
```
Output:
```bash
{MacBook Air 900 true}
```