The `database/sql` package is a native implementation in [[Go]] that exposes an interface to manage [[Database]] connections and operations.
## Key features:
- **Part of Go's standard libraries**.
- **Compatible with SQL databases**.
- **Requires a corresponding database driver**.
- Uses the `sql.DB` type to manage connections and executions.
- Can manage a single connection or a connection pool.
## Implementation
### Installation:
To use `database/sql`, we need to install the corresponding driver for the database we intend to connect to. In this case, we are using **MySQL**. Therefore, we install the MySQL driver:
```sh
go get "github.com/go-sql-driver/mysql"
```
When importing the driver, we need to use the underscore (`_`) to indicate that we are importing the package for its side effects (i.e., registering the driver), even if we don’t use the package directly:
```go
import (
    "database/sql"
    _ "github.com/go-sql-driver/mysql"
)
```
### Usage:
The `Open` function from the `sql` package takes two parameters: the name of the driver (hence, the need to import it) and the connection string for the database. It returns a connection object and an error (if any).
Example:
```go
func init() {
  dataSource := "user:pass@tcp(server:Port)/dbName"
  // Open initializes a connection pool. Only open once.
  storageDB, err = sql.Open("mysql", dataSource)
  if err != nil {
    panic(err)
  }
}
```
In this example, the `init` function establishes the connection and exports the `StorageDB` variable as a pointer of type `*sql.DB`, created using the connection details. This way, whenever we need to interact with the database, we can simply refer to the `StorageDB` variable.
## Full example
```go
package db

import (
    "database/sql"
    "log"

    _ "github.com/go-sql-driver/mysql"
)

var (
    StorageDB *sql.DB
)

func init() {
    dataSource := "root:abcd1234@tcp(localhost:3306)/storage"
    // Open initializes a connection pool. Only open once.
    var err error
    StorageDB, err = sql.Open("mysql", dataSource)
    if err != nil {
        panic(err)
    }
    if err = StorageDB.Ping(); err != nil {
        panic(err)
    }
    log.Println("Database configured")
}
```
## Connection String Details
The necessary information for the database connection includes:
- **DB User**
- **Password**
- **Server**
- **Port**
- **DB Name**
You can define the connection details as a string, like this:
```go
dataSource := "root:password@tcp(localhost:3306)/database_name"
```
## General Considerations
1. **Connection Pool Management**: The `database/sql` package manages the connection pool. Reopening connections using `Open` should be avoided, as it can lead to memory leaks and connection saturation.
2. **Separate Connection Setup**: It's a good practice to handle connection setup in a separate file.
3. **Database-Specific Drivers**: Each database engine works differently, despite some common functionalities. Always import the appropriate driver for your database.