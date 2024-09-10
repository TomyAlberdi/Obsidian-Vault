Up to this point, we have studied that to begin solving a problem using the object-oriented paradigm, we must go through a process to identify objects, which we can call the abstraction process. During this, we not only identify the parts that make up our "universe" or "domain" according to the context but also how these parts interact through relationships. This is how we define classes, with their attributes and operations. Additionally, we define what each part must do to contribute to solving the problem, that is, we establish the responsibilities of the classes. In this class, we will see the inheritance relationship and its benefits.
**Inheritance** is one of the pillars of the object-oriented paradigm, also known as an "is-a" relationship. We can say that inheritance is an ordering between classes. A class that inherits from another adds to its own attributes and methods those of the class it inherits from.
### Utility:
Inheritance promotes code reuse.
**Example**: Employee hierarchy.
- **Manager**: In addition to the attributes `promotionDate` and `budgetAmount`, it has the attributes `name`, `address`, and `salary` inherited from `Employee`, as well as the methods `enter()` and `exit()`.
- **Project Manager**: In addition to the attribute `projectType` and the method `planProject()`, it has all the attributes and methods of `Manager` and `Employee`.
### Multiple Inheritance:
It is established when a class inherits from several other classes. In this case, the child class inherits attributes and responsibilities from the different parent classes. The use of multiple inheritance requires very careful consideration to avoid functional overlap of attributes and responsibilities. This is why multiple inheritance is not allowed in Java and, as it is not considered a good design practice, it will not be used in this course.
## Inheritance in [[Java]]
We saw that there is another type of relationship between classes that allows us to model classes that inherit everything from their superclass, including attributes and behavior, i.e., attributes and methods. We only need to add the specific characteristics and new responsibilities we require. Let's see how this is done in code.
#### Extends and Super:
In Java, inheritance is indicated by placing the keyword `extends` in the child class, followed by the name of the parent class:
```java
public class Employee extends Person {}
```
Both the superclass and the subclass have a constructor, but each one must handle its own attributes.
In the case of the subclass, before working with its own attributes, it is necessary to instantiate the attributes of the superclass. Therefore, the first thing done in the constructor of a subclass is to invoke the constructor of the superclass, respecting its parameters. This is done using the `super()` function:
```java
public class Employee extends Person {
  private double salary;
  private String employeeID;
  public Employee(String name, String idNumber, String employeeID) {
    super(name, idNumber);
    this.employeeID = employeeID;
    this.salary = 30000;
  }
}
```