Created: 2024-09-17 15:17
## Family Tree:
1. Computer
2. Backend Development
3. Go
4. [[Go Web]]
-- -
In Go, Repositories are components that encapsulate the logic necessary for accessing a data source. They centralize common data access functionality, which improves maintainability and decouples the infrastructure or technology used to access databases from the domain model.
## Implementation
First, we need to define an interface that contains the method signatures that can be called within our domain. In the following example, you can find a simple interface that defines the CRUD methods.
By defining **Repository** as this interface, we can use it throughout the domain layer. This interface always returns our entities, in this case, the `Product`.
### Repository Interface:
```go
// Repository Interface
type Repository interface {
    Store(name, productType string, count int, price float64) (models.Product, error)
    GetOne(id int) models.Product
    Update(product models.Product) (models.Product, error)
    GetAll() ([]models.Product, error)
    Delete(id int) error
}
```
### Repository Implementation:
```go
type repository struct {}

// NewRepo returns a new instance of the repository that implements the Repository interface.
func NewRepo() Repository {
    return &repository{}
}
```
### Product Struct:
The `Product` struct represents the data model that will be managed by the repository.
```go
// Struct Product
type Product struct {
    ID    int     `json:"id"`
    Name  string  `json:"nombre"`
    Type  string  `json:"tipo"`
    Count int     `json:"cantidad"`
    Price float64 `json:"precio"`
}
```
### Usage in Services:
The designed **Repository** interface is used by the **Service** layer to orchestrate or manage each of the processes required. The service calls the repository's methods to handle data manipulation.
The interface must satisfy the various needs for reading, writing, updating, and deleting records in the database.
## CRUD Methods
Here’s an overview of how the repository methods are implemented in Go to interact with a MySQL database. These methods handle basic CRUD operations—**GetOne**, **Store**, **Update**, and **Delete**—for the `User` model using the `database/sql` package.
### `GetOne`
The `GetOne` function is used to retrieve a specific record (in this case, a user) from the database based on the `id`.
```go
func (r *repository) GetOne(id int) models.User {
    var user models.User
    db := db.StorageDB
    rows, err := db.Query("SELECT * FROM users WHERE id = ?", id)
    if err != nil {
        log.Println(err)
        return user
    }
    for rows.Next() {
        if err := rows.Scan(&user.ID, &user.Name, &user.Telephone, &user.Email, &user.Address); err != nil {
            log.Println(err.Error())
            return user
        }
    }
    return user
}
```
#### Key Functions:
- **`db.Query`**: Executes the SQL query and returns rows for the given query.
- **`rows.Next`**: Iterates through the rows returned by the query.
- **`rows.Scan`**: Maps the columns of the row into the provided variables.
### `Store` Method:
The `Store` function allows users to insert a new record into the database.
```go
func (r *repository) Store(user models.User) (models.User, error) {
    db := db.StorageDB
    stmt, err := db.Prepare("INSERT INTO users(name, email, telephone, address) VALUES( ?, ?, ?, ?)")
    if err != nil {
        log.Fatal(err)
    }
    defer stmt.Close()

    var result sql.Result
    result, err = stmt.Exec(user.Name, user.Email, user.Telephone, user.Address)
    if err != nil {
        return models.User{}, err
    }

    insertedId, _ := result.LastInsertId()
    user.ID = int(insertedId)
    return user, nil
}
```
#### Key Functions:
- **`db.Prepare`**: Prepares the SQL statement for execution.
- **`stmt.Exec`**: Executes the prepared statement with the provided input values and returns the result, which includes the inserted record’s ID.
### `Update` Method:
The `Update` function modifies an existing record in the database.
```go
func (r *repository) Update(user models.User) (models.User, error) {
    db := db.StorageDB
    stmt, err := db.Prepare("UPDATE users SET name = ?, email = ?, telephone = ?, address = ? WHERE id = ?")
    if err != nil {
        log.Fatal(err)
    }
    defer stmt.Close()

    _, err = stmt.Exec(user.Name, user.Email, user.Telephone, user.Address, user.ID)
    if err != nil {
        return models.User{}, err
    }
    return user, nil
}
```
#### Key Functions:
- **`db.Prepare`**: Prepares the update SQL query.
- **`stmt.Exec`**: Executes the prepared update statement with the given values for the user.
### `Delete` Method:
The `Delete` function removes a record from the database based on the user’s `id`.
```go
func (r *repository) Delete(user models.User) error {
    db := db.StorageDB
    stmt := "DELETE FROM users WHERE id = ?"
    _, err := db.Exec(stmt, user.ID)
    if err != nil {
        return err
    }
    return nil
}
```
#### Key Function:
- **`stmt.Exec`**: Executes the delete statement to remove the record based on the user’s ID.