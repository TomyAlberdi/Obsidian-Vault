Created: 2024-09-17 17:30
## Family Tree:
1. Computer
2. Programming Theory
3. Object-Oriented Programming
4. [[Design Patterns]]
-- -
The Factory design pattern (Design Patterns) is one of the main design patterns and one of the most widely used in most programming languages today. It has two variations:
- **Factory Method**:
  This variation defines an interface (Development/Backend Development/Java/Interfaces) for creating an object but allows subclasses to decide which class to instantiate. These construction factories minimize the use of the `new` keyword, encapsulate the initialization process, and manage different concrete implementations. Additionally, this centralization reduces the impact of adding or removing concrete classes in the system and the effects of dependencies on concrete classes.
- **Abstract Factory**:
  This variation provides an interface for creating families of dependent or related objects without specifying their concrete classes. Thus, the Abstract (Abstract Class) Factory encapsulates a group of factories and controls how the client accesses these factories.
## Factory Method
#### UML:
![](https://t12904266.p.clickup-attachments.com/t12904266/316ee73a-1bd3-4c8d-83d3-433db063b230/image.png)
- **Creator (Abstract Creator):** Declares the Factory Method that returns an object of the `Product` class. This element can also define a base implementation that returns an object of the `ConcreteProduct` class.
- **ConcreteCreator (Concrete Creator):** Overrides the method that manufactures the `Product`, allowing us to instantiate the `ConcreteProduct` without directly referencing it.
- **Product (Abstract Product):**  Defines an interface for objects created by the Factory Method.
- **ConcreteProduct (Concrete Product):** Represents an implementation for the product interface.
## Abstract Factory Method
#### UML:
![](https://t12904266.p.clickup-attachments.com/t12904266/b13f2815-306f-4e5b-9393-5b9f852993db/image.png)
- **AbstractFactory:** Its purpose is to declare creation methods of type `AbstractProduct`, which are implemented by a `ConcreteFactory` class that inherits or implements `AbstractFactory`.
- **AbstractProduct:** Declares methods implemented by classes of type `ConcreteProduct`. `ConcreteFactory` internally creates an object of type `ConcreteProduct`, but this object is returned as `AbstractProduct`.
- **ConcreteFactory:** Implements the methods declared in `AbstractFactory`, creating an object of type `ConcreteProduct` and returning it as `AbstractProduct`.
- **ConcreteProduct:** This class specifies the correct instance to create. It implements the methods declared in `AbstractProduct`.
## Conclusion
The purpose of the Factory pattern is to create objects, which is why it is considered a creational pattern (Design Patterns > Creation Patterns). Essentially, the creation logic is encapsulated within the factory (`FactoryMethod`), and a method is provided that returns an object (the default Factory Method), or the object creation is delegated to a subclass (the default Abstract Factory Method).
## Example
In this example, we will implement the Factory Method pattern by creating a soda factory that constructs different types of sodas depending on the implementation of its subclasses.
#### Abstract Product Class:
```java
public abstract class Soda {
  private String name;
  
  public String getName() { 
    return name; 
  }
  
  public void open() {
    // Implementation for opening the soda
  }
}
```
#### Concrete Product Classes:
Each concrete product inherits from the main abstract class.
```java
public class Cola extends Soda {
  String name = "Coca Cola";
  
  @Override
  public String getName() { 
    return name; 
  }
  
  @Override
  public void open() { 
    super.open(); 
  }
}

public class Orange extends Soda {
  String name = "Orange Fanta";
  
  @Override
  public String getName() { 
    return name; 
  }
  
  @Override
  public void open() { 
    super.open(); 
  }
}
```
#### Factory Class:
```java
public class SodaFactory {
  public static Soda build(String type) {
    switch(type) {
      case "Cola":
        return new Cola();
      case "Orange":
        return new Naranja();
      default:
        return null;
    }
  }
}
```
### Execution:
We create three instances using the static `build()` method of the `SodaFactory` class. Two of the products are valid, but the third one isn't created because that type of soda doesn't exist.
```java
public static void main(String[] args) {
  Soda s1 = SodaFactory.build("Cola");
  Soda s2 = SodaFactory.build("Orange");
  Soda s3 = SodaFactory.build("Grape");
}
```
Upon compilation, you will see how, by simply passing the appropriate parameter to the factory, the corresponding subclass is used without the client needing to specify it. We also handle an exception with a try-catch block:
```java
public static void main(String[] args) {
  try {
	Soda s1 = SodaFactory.build("Cola");
	Soda s2 = SodaFactory.build("Orange");
	Soda s3 = SodaFactory.build("Grape");
  } catch (Exception e) {
    System.out.println("Exception: " + e);
  }
}
```
In this code, the `SodaFactory` ensures that only the sodas specified in the switch cases can be created. If an invalid type is passed (e.g., "Grape"), the factory returns `null`, and this can be caught and handled by the exception block.