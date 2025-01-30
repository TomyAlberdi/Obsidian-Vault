Created: 2024-09-30 16:36
## Family Tree:
1. Computer
2. Backend Development
3. [[Java]]
-- -
Hibernate is an **ORM** (Object-Relational Mapping) framework that facilitates data persistence, specifically with relational databases (RDBMS).
## Persistence
Persistence refers to ensuring that the data from our application survives the lifecycle of the application. In Java, this means keeping the state of objects alive beyond the scope of the JVM, so that the same state is available later.
Hibernate maps Java classes to database tables and provides mechanisms for querying data. The mapping is done either through an `.xml` configuration file or annotations. If a database change is needed, only the configuration file or annotations need to be updated.
## Features
- **Open-source**: It uses minimal resources.
- **High performance**: Hibernate is fast because it internally uses caching mechanisms.
- **Database-independent queries**: Using HQL (Hibernate Query Language), it's possible to generate queries that are independent of the database being used. Before Hibernate, if the database was changed, all the queries in the application had to be updated.
- **Automatically created tables**.
- **Simplified complex joins**: It can fetch data from multiple tables.
- **Provided statistics**: via query cache and database status.
## Annotations
Annotations provide a powerful way to add metadata for mapping objects to relational tables. This metadata is injected into the Java POJO class alongside the code. Below are some key annotations that belong to the **JPA standard** and are used by Hibernate.
### `@Entity`:
Marks the class as an entity bean, indicating that it will be mapped by the ORM to a database table.
### `@Table`:
Specifies the details of the table used to persist the entity in the database. The `name` attribute can be used to explicitly specify the table name. If the table name matches the class name, this annotation is not necessary.
### `@Id`:
Every entity bean must have a primary key (which can be simple or compisite). This annotation specifies which field is the primary key, and the database generates a new value for each insert operation.
#### `@GeneratedValue`:
This annotation manages how the primary key value is generated. If not used, the application is responsible for managing the `@Id` field. The `strategy = GenerationType` attribute can have the following values:
- **AUTO**: The default type, the generated Id can be numeric or UUID.
- **IDENTITY**: Assigns primary keys using an identity column, which auto-increments.
- **SEQUENCE**: Assigns primary keys using a customizable sequence.
- **TABLE**: Assigns primary keys using a database table that stores the last primary key value.
### `@Column`:
Specifies the details of a column to indicate which field or attribute is mapped. It can be used with the following attributes:
- **name**: Explicitly specifies the column name.
- **length**: Specifies the column size, especially useful for `String` fields. For example, `length = 3` generates a column of type `VARCHAR(3)`. Attempting to insert a longer string would result in a SQL error.
- **nullable**: Marks the column as non-nullable with `nullable = false` when generating the schema.
- **unique**: Ensures only unique values are allowed in the column.
## Relationships
For each relationship type in a database, we have an equivalent annotation in JPA and Hibernate:

| Relationship | Annotation    |
| ------------ | ------------- |
| One to one   | `@OneToOne`   |
| One to many  | `@OneToMany`  |
| Many to one  | `@ManyToOne`  |
| Many to many | `@ManyToMany` |
### One to one:
User-Address relationship.
#### Unidirectional:
```java
@Entity
@Table(name = "users")
public class User {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "id")
    private Long id;

    @OneToOne(cascade = CascadeType.ALL)
    @JoinColumn(name = "address_id", referencedColumnName = "id")
    private Address address;
    
    // Getters and setters
}
```
- **`@OneToOne`** indicates a one-to-one relationship with the `Address` entity.
- **`@JoinColumn`** has two parameters:
    - `name`, which defines the name of the column in the `users` table that maps to the primary key of the `addresses` table.
    - `referencedColumnName`, which refers to the name of the primary key in the `addresses` table.
```java
@Entity
@Table(name = "addresses")
public class Address {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "id")
    private Long id;
    
    // Getters and setters
}
```
Since the relationship is **unidirectional**, we do not add a `User` attribute in the `Address` class.
#### Bidirectional:
```java
@Entity
@Table(name = "users")
public class User {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "id")
    private Long id;

    @OneToOne(cascade = CascadeType.ALL)
    @JoinColumn(name = "address_id", referencedColumnName = "id")
    private Address address;
    
    // Getters and setters
}
```
The `@OneToOne` annotation indicates the one-to-one relationship with the `Address` entity. `@JoinColumn` works similarly to the unidirectional example.
```java
@Entity
@Table(name = "addresses")
public class Address {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "id")
    private Long id;

    @OneToOne(mappedBy = "address")
    private User user;

    // Getters and setters
}
```
In the bidirectional case, the `mappedBy` attribute in the `@OneToOne` annotation tells Hibernate that the `address` attribute in the `User` class owns the relationship.
### One to many:
Cart-Items relationship.
#### Unidirectional:
```java
@Entity
@Table(name = "carts")
public class Cart {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "id")
    private Long id;

    @OneToMany(cascade = CascadeType.ALL)
    @JoinColumn(name = "cart_id")
    private Set<Item> items;

    // Getters and setters
}
```
To define a **one-to-many unidirectional** relationship, we use the `@OneToMany` annotation. The `@JoinColumn` is located on the "one" side of the relationship, referencing the foreign key (`cart_id`) in the "many" side (the `Item` table). In this example, we have two tables: **Cart** and **Items**. The `@JoinColumn` annotation in the `Cart` class refers to the foreign key of the `Items` table.
```java
@Entity
@Table(name = "items")
public class Item {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "id")
    private Long id;

    // Getters and setters
}
```
In the above code, the `Item` class does not have an attribute referencing `Cart`, as the relationship is navigable only from `Cart` to `Item`.
#### Bidirectional:
```java
@Entity
@Table(name = "carts")
public class Cart {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "id")
    private Long id;

    @OneToMany(mappedBy = "cart")
    @JsonIgnore
    private Set<Item> items;

    // Getters and setters
}
```
In a **bidirectional** relationship, the `mappedBy` attribute in the `@OneToMany` annotation indicates that the `cart` attribute in the `Item` class establishes the relationship. We use the `@JsonIgnore` annotation to prevent potential infinite loops when the object is serialized to JSON (in the case of bidirectional relationships).
```java
@Entity
@Table(name = "items")
public class Item {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "id")
    private Long id;

    @ManyToOne
    @JoinColumn(name = "cart_id")
    private Cart cart;

    // Getters and setters
}
```
In the bidirectional relationship, the `Item` class now includes a reference to the `Cart` class using the `@ManyToOne` annotation, establishing the other side of the relationship.
### Many to many:
Contacts-Photos relationship.
#### Unidirectional:
```java
@Entity
@Table(name = "contacts")
public class Contact {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "id")
    private Long id;

    @ManyToMany
    @JoinTable(
        name = "likes",  // Name of the associative table
        joinColumns = @JoinColumn(name = "contact_id"),  // Column in "likes" table pointing to "Contact"
        inverseJoinColumns = @JoinColumn(name = "photo_id")  // Column in "likes" table pointing to "Photo"
    )
    private Set<Photo> likedPhotos;

    // Getters and setters
}
```
- **`@ManyToMany`**: Indicates a many-to-many relationship with the `Photo` class.
- **`@JoinTable`**: Defines the associative table (`likes`) that maps the relationship between `Contact` and `Photo`. The `joinColumns` refers to the column that stores the foreign key of the owning entity (`Contact`), and the `inverseJoinColumns` refers to the foreign key of the related entity (`Photo`).
```java
@Entity
@Table(name = "photos")
public class Photo {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "id")
    private Long id;

    // Getters and setters
}
```
In this example, the `Photo` class does not have a collection of `Contact` elements because the relationship is **unidirectional**. The relationship is navigable only from `Contact` to `Photo`.
#### Bidirectional:
```java
@Entity
@Table(name = "contacts")
public class Contact {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "id")
    private Long id;

    @ManyToMany
    @JoinTable(
        name = "likes",  // Name of the associative table
        joinColumns = @JoinColumn(name = "contact_id"),  // Column in "likes" table pointing to "Contact"
        inverseJoinColumns = @JoinColumn(name = "photo_id")  // Column in "likes" table pointing to "Photo"
    )
    @JsonIgnore
    private Set<Photo> likedPhotos;

    // Getters and setters
}
```
- **`@ManyToMany`**: Indicates a many-to-many relationship with the `Photo` class.
- **`@JoinTable`**: Specifies the name of the associative table (`likes`), and the columns that store foreign keys (`contact_id` for `Contact`, and `photo_id` for `Photo`).
- **`@JsonIgnore`**: Used to avoid an infinite loop when serializing the object to JSON in a bidirectional relationship.
```java
@Entity
@Table(name = "photos")
public class Photo {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    @Column(name = "id")
    private Long id;

    @ManyToMany(mappedBy = "likedPhotos")
    private Set<Contact> contacts;

    // Getters and setters
}
```
In the bidirectional relationship, the `Photo` class has a collection of `Contact` objects. The **`mappedBy`** attribute in the `@ManyToMany` annotation indicates that the `likedPhotos` attribute in the `Contact` class owns the relationship.
### Fetch type
In Hibernate, it's necessary to specify a **FetchType** when using associations (relationships) because it defines when data is retrieved from the database and loaded into memory.
When Hibernate accesses an entity that is related to another entity through associations, the timing of when the related data is retrieved can be controlled by the **FetchType** setting. The two main types are:
- EAGER
- LAZY
Example:
```java
public class Address {
    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private int id;
    private String street;
    private int houseNumber;
    private String city;
    private int zipCode;

    @ManyToOne(fetch = FetchType.LAZY)  // Specifies lazy loading for the person association
    private Person person;
}
```
#### Eager fetching:
Eager fetching is a design pattern where the initialization of data occurs immediately when the entity is fetched.
In Eager loading, the records and their associated entities mapped through relationships are loaded in memory immediately during the same query.
Example: Eager loading in `Cart` and `Item` classes:
```java
@OneToMany(mappedBy = "cart", cascade = CascadeType.ALL, fetch = FetchType.EAGER)
private Set<Item> items;
```
In this example, when fetching a `Cart` by its `id` with eager loading, both the `Cart` and its associated `Item` entieties are fetched in a single query. You can see the following output in the console:
```
Hibernate: 
select cart0_.id as id1_1_0_, items1_.cart_id as cart_id4_4_1_, 
items1_.id as id1_4_1_, items1_.id as id1_4_2_, 
items1_.cantidad as cantidad2_4_2_, items1_.cart_id as cart_id4_4_2_, 
items1_.descripcion as descripc3_4_2_ from cart cart0_ 
left outer join items items1_ on cart0_.id=items1_.cart_id where cart0_.id=?
```
#### Lazy fetching:
Lazy fetching is a design pattern where the initialization of an object is delayed until it is exmplicitly needed.
In Lazy loading, associated entities are not loaded into memory until there is an explicit call to retrieve them (e.g., calling a `get` method).
Example: Lazy loading in `Cart` and `Item` classes:
```java
@OneToMany(mappedBy = "cart", cascade = CascadeType.ALL, fetch = FetchType.LAZY)
private Set<Item> items;
```
In this example, when fetching a `Cart` by its `id` with lazy loading, only the `Cart` entity is fetched initially. The `Item` entities are only loaded when they're explicitly accessed. You can see the following output in the console:
1. The initial query to fetch the `Cart`:
```
Hibernate: 
select cart0_.id as id1_1_0_ from cart cart0_ where cart0_.id=?
```
2. The subsequent query to fetch the `Item` entities when they're accessed:
```
Hibernate: 
select items0_.cart_id as cart_id4_4_0_, items0_.id as id1_4_0_, 
items0_.id as id1_4_1_, items0_.cantidad as cantidad2_4_1_, 
items0_.cart_id as cart_id4_4_1_, items0_.descripcion as descripc3_4_1_ 
from items items0_ where items0_.cart_id=?
```
#### Performance considerations:
- Eager loading can cause performance issues in scenarios where unnecessary data is loaded onto memory, especially in cases where many related entities exist.
- Lazy loading provides faster loading times and consumes less memory compared to eager loading. By default, Lazy is the fetch type of the `@OneToMany` and `@ManyToMany` associations, which helps avoid the performance pitfalls of eager loading when it's not needed.

## Complete example:
```java
@Entity
@Table(name = "Author")
public class Author {

    @Id
    @GeneratedValue(strategy = GenerationType.SEQUENCE)
    private Long id;

    @Column(name = "first_name", length = 50, nullable = false)
    private String firstName;

    @Column(name = "last_name", length = 50, nullable = false)
    private String lastName;

    @OneToMany(mappedBy = "author")
    private Set<Publication> publications = new HashSet<>();
}

@Entity
@Table(name = "Publication")
public class Publication {

    @Id
    @GeneratedValue(strategy = GenerationType.SEQUENCE)
    private Long id;

    @Column(name = "version")
    private int version;

    @Column(name = "title", length = 255, nullable = false)
    private String title;

    @ManyToOne(fetch = FetchType.LAZY)
    private Author author;

    @Column(name = "publishing_date")
    private LocalDate publishingDate;
}
```