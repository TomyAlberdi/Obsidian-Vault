Created: 2024-09-26 19:02
## Family Tree:
1. Computer
2. Programming Theory
3. Object-Oriented Programming
4. [[Design Patterns]]
-- -
The **DAO (Data Access Object) pattern** helps decouple the data itself from the storage technology. In other words, the system is indifferent to whether we use PostgreSQL or MySQL because, in either case, the communication method remains the same.
## Solution
This pattern proposes the following approach:
1. **Create an interface** where we define all the operations we want to perform, usually the most common ones like create, update, delete, and read (CRUD operations).
2. **Create different implementations** of this interface, for example, one implementation for PostgreSQL and another for MySQL.
This way, the **business layer** (where the core logic of the system resides) communicates with the **persistence layer** but doesn’t know the implementation details. It won’t matter whether we use PostgreSQL or MySQL because both implementations will have the same methods defined in the interface.
In a system, a **layer** refers to a grouping of components (classes) with similar responsibilities.
## UML Diagram
![[Programming Theory/Object-Oriented Programming/Design Patterns/attachments/image.png]]- **Entity**: These are the business classes, for example, `Student`, `Course`, `Account`, etc.
- **ServiceEntity Classes**: For each entity, there will be a service class. These service classes are used by the presentation layer and allow us to decouple data access from the view.
- **DAO Interface**: This is the interface that forces DAO classes that implement it to provide the operations we need to perform on the database.
- **DAO Entity Classes**: These classes implement the DAO interface and handle all database operations for a specific database (e.g., H2). If we later switch to MySQL or MongoDB, we would create a new class (e.g., `DAOEntityMongoDB`), which implements the same interface but with different code for each method than `DAOEntityH2`.
## Benefits
- **ServiceEntity classes**: As shown in the class diagram, each service class has a reference (i.e., an attribute called `dao` of type `DAO`). This attribute can be any class that implements the DAO interface. This allows us to change the persistence mechanism more easily and dynamically by simply pointing the service class to the new DAO (dynamic binding).
- **DAO implements the Strategy pattern**: You may have noticed that DAO uses the **Strategy pattern**, where we have different persistence strategies represented by our DAO classes.
## Example
### DAO Interface:
```java
public interface StudentDAO {
    void create(Student student);
    Student read(int id);
    void update(Student student);
    void delete(int id);
}
```
### DAO Implementation for PostgreSQL:
```java
public class PostgresStudentDAO implements StudentDAO {
    @Override
    public void create(Student student) {
        // PostgreSQL-specific implementation
    }

    @Override
    public Student read(int id) {
        // PostgreSQL-specific implementation
        return null;
    }

    @Override
    public void update(Student student) {
        // PostgreSQL-specific implementation
    }

    @Override
    public void delete(int id) {
        // PostgreSQL-specific implementation
    }
}
```
### DAO Implementation for MySQL:
```java
public class MySQLStudentDAO implements StudentDAO {
    @Override
    public void create(Student student) {
        // MySQL-specific implementation
    }

    @Override
    public Student read(int id) {
        // MySQL-specific implementation
        return null;
    }

    @Override
    public void update(Student student) {
        // MySQL-specific implementation
    }

    @Override
    public void delete(int id) {
        // MySQL-specific implementation
    }
}
```
### Service Layer:
```java
public class StudentService {
    private StudentDAO dao;

    public StudentService(StudentDAO dao) {
        this.dao = dao;
    }

    public void createStudent(Student student) {
        dao.create(student);
    }

    public Student getStudent(int id) {
        return dao.read(id);
    }

    public void updateStudent(Student student) {
        dao.update(student);
    }

    public void deleteStudent(int id) {
        dao.delete(id);
    }
}
```
### Usage:
```java
public class MainApp {
    public static void main(String[] args) {
        StudentDAO dao = new PostgresStudentDAO(); // Use PostgreSQL implementation
        StudentService service = new StudentService(dao);

        Student student = new Student();
        service.createStudent(student);
    }
}
```
In this example, switching from **PostgresStudentDAO** to **MySQLStudentDAO** is seamless and requires no changes in the service or business layer, demonstrating the flexibility and modularity provided by the DAO pattern.
By using this pattern, we make the persistence layer interchangeable and scalable, allowing us to switch databases or storage mechanisms without affecting other layers of the system.