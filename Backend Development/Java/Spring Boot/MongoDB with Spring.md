Created: 2024-09-30 18:25
## Family Tree:
1. Computer
2. Backend Development
3. Java
4. [[Spring Boot]]
-- -
## Annotations
Here are some key annotations used in **Spring Data MongoDB**, similar to those in **JPA** but tailored for MongoDB's document-based architecture:
### `@Document`
- **Usage**: Placed on a class, this annotation tells the **MongoDriver** that objects of this class can be treated as Mongo documents within a specific collection.
- **Details**: By default, the collection name is derived from the class name. If the collection name is different, it must be explicitly specified.
```java
@Document(collection = "airplanes")
public class Aircraft {
    private String id;
    private String model;

    @Field(name = "seats")
    private int nbSeats;
}
```
This example maps the `Aircraft` class to the `airplanes` collection, with the `nbSeats` field being saved as `seats` in MongoDB.
### `@Id`
- **Usage**: Every document in a MongoDB collection must have an `id` field. It acts like a primary key, is unique, and indexed automatically.
```java
@Document
public class Aircraft {
    @Id
    private String id;
    private String model;
    @Transient
    private int nbSeats;  // This field won't be persisted
}
```
### `@Transient`:
- **Usage**: Used to exclude a field from being persisted to the MongoDB database. It's useful when certain fields should only exist in the runtime but should not be stored.
### `@Indexed`:
- **Usage**: This annotation is applied to a field when we want to create an index on it for faster querying. We can also specify the index direction (`ASCENDING` or `DESCENDING`) and whether the field should be unique.
```java
@Document
public class Aircraft {
    @Id
    private String id;

    @Indexed(direction = IndexDirection.ASCENDING, unique = false)
    private String model;

    private int nbSeats;
}
```
In this example, the `model` field is indexed to improve the query performance on this field.
### `@DbRef`:
- **Usage**: Acts similarly to a **join** in relational databases. It links a document in one collection to another document in a different collection.
```java
@Document
public class Manufacturer {
    @Id
    private String id;
    private String name;
}

@Document
public class Aircraft {
    @Id
    private String id;
    private String model;

    @DbRef
    private Manufacturer man;
}
```
In this example, `Aircraft` references a `Manufacturer` through the `@DbRef` annotation, which links the `Manufacturer` document to the `Aircraft` document.
## Complete example
Here’s a complete example of how to map the `Book` class to the `books` collection in MongoDB, implement a `BookRepository`, create a `BookService`, and expose a `BookController` through a REST API. Additionally, we'll see how to implement a custom query that filters books by author.
### `Book` entity:
```java
import org.springframework.data.annotation.Id;
import org.springframework.data.mongodb.core.mapping.Document;
import org.springframework.data.mongodb.core.mapping.Field;

@Document(collection = "books")
public class Book {

    @Id
    private String id;
    private String author;

    @Field(name = "book")
    private String bookTitle;

    // Getters and setters
    public String getId() {
        return id;
    }

    public void setId(String id) {
        this.id = id;
    }

    public String getAuthor() {
        return author;
    }

    public void setAuthor(String author) {
        this.author = author;
    }

    public String getBookTitle() {
        return bookTitle;
    }

    public void setBookTitle(String bookTitle) {
        this.bookTitle = bookTitle;
    }
}
```
- The `@Document` annotation marks the class as a MongoDB document, specifying the collection name `books`.
- The `@Id` annotation marks the `id` field as the document's unique identifier.
- The `@Field(name = "book")` annotation specifies that the `bookTitle` field in Java maps to the `book` field in MongoDB.
### `BookRepository`:
```java
import org.springframework.data.mongodb.repository.MongoRepository;
import org.springframework.stereotype.Repository;
import java.util.List;

@Repository
public interface BookRepository extends MongoRepository<Book, String> {

    // Custom query to find books by author
    List<Book> findBooksByAuthor(String author);
}
```
- `BookRepository` extends `MongoRepository`, which provides built-in CRUD operations for the `Book` entity.
- The method `findBooksByAuthor` is a query method that filters books based on the `author` field in the database.
### `BookService`:
```java
import org.springframework.stereotype.Service;
import java.util.List;

@Service
public class BookService {

    private final BookRepository bookRepository;

    public BookService(BookRepository bookRepository) {
        this.bookRepository = bookRepository;
    }

    public List<Book> findAllBooks() {
        return bookRepository.findAll();
    }

    // Method to find books by author
    public List<Book> findBooksByAuthor(String author) {
        return bookRepository.findBooksByAuthor(author);
    }
}
```
- `BookService` handles the business logic and interacts with `BookRepository` to fetch all books and filter books by author.
### `BookController`:
```java
import org.springframework.web.bind.annotation.*;
import java.util.List;

@RestController
@RequestMapping(value = "/mongoexample")
public class BookController {

    private final BookService bookService;

    public BookController(BookService bookService) {
        this.bookService = bookService;
    }

    // GET request to retrieve all books
    @GetMapping(value = "/books")
    public List<Book> getAllBooks() {
        return bookService.findAllBooks();
    }

    // GET request to retrieve books by author
    @GetMapping(value = "/books/author")
    public List<Book> getBooksByAuthor(@RequestParam String author) {
        return bookService.findBooksByAuthor(author);
    }
}
```
- The `@RestController` annotation defines the `BookController` as a REST API.
- The `@RequestMapping("/mongoexample")` maps all routes starting with `/mongoexample`.
- The `@GetMapping("/books")` endpoint retrieves all books.
- The `@GetMapping("/books/author")` endpoint retrieves books filtered by the `author` query parameter.
### Custom Query example:
To filter books by author using a custom query, you pass the author's name as a query parameter:
```
GET http://localhost:8080/mongoexample/books/author?author=Brandon Sanderson
```
This triggers the `findBooksByAuthor` method in `BookRepository`, which performs the query in MongoDB to return a list of books written by that author.