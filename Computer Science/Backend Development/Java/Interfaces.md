Created: 2024-09-17 15:44
## Family Tree:
1. Computer
2. Backend Development
3. [[Java]]
-- -
Interfaces are "is-a" relationships, very similar to abstract classes (Abstract Class). They are defined using the `interface` keyword instead of `class`. All methods in an interface are abstract, so the `abstract` keyword is not necessary, and like abstract classes, the methods do not have a body.
An interface establishes a contract. Any class that implements an interface is required to implement all the methods of that interface.
A class can only inherit from one superclass, but it can implement multiple interfaces.
### Interfaces and Inheritance:
When we inherit from a class, we add the attributes and behaviors of the parent class. However, when we implement an interface, we are only requiring the class that implements it to override (implement) the methods of the interface.
Both inheritance and interfaces share the "is-a" relationship type, which means both allow us to perform dynamic binding and, consequently, polymorphism.
What interfaces enable is the ability to break free from a hierarchy and add behavior to a class that cannot be inherited from a higher level in the hierarchy, as it is "added" laterally. This even allows for mixing both mechanisms.
Example:
```java
public class Person implements Hugable {
  @Override
  public void hug() {
    // Mandatory implementation of the method inherited from the "Hugable" interface
  }
}
```
## Interface `Comparable`
When comparing primitive types, we use operators like `<`, `>`, `==`, etc. But how do we compare two objects?
To compare two objects, the first thing we need to determine is which attribute(s) we will use for the comparison.
We’ve already seen that we can solve this problem by overriding the `equals()` method. However, this method only helps us compare equality, not to determine if one object is "greater" or "lesser" than another.
Another solution to this problem is to ensure that all the objects we need to compare have, for example, a `compareWith` method. This method would take as a parameter the other object to compare against and return:
- Zero if they are equal.
- A number greater than zero if the invoking object is greater than the one passed as a parameter.
- A number less than zero if the invoking object is lesser than the one passed as a parameter.
With interfaces, we can ensure that any class implementing it must have a `compareWith` method and can define its own implementation.
We don't need to create an interface to compare objects because Java already provides the `Comparable` interface, which is necessary in various scenarios, such as sorting objects in collections. To implement this interface, we need to import the `java.lang` package.
The method that the `Comparable` interface requires to be implemented is called `compareTo`.
Example:
```java
public class Dog implements Comparable<Dog> {
  private Double weight;

  @Override
  public int compareTo(Dog other) {
    int result = 0;
    if (this.getWeight() > other.getWeight()) { 
      result = 1; 
    } 
    if (this.getWeight() < other.getWeight()) { 
      result = -1; 
    }
    return result;
  }

  public Double getWeight() {
    return weight;
  }
  // Other methods and constructors
}
```
In this example, the `Dog` class implements `Comparable<Dog>` and overrides the `compareTo` method to compare `Dog` objects based on their weight. The method returns `1` if the current dog is heavier, `-1` if it’s lighter, and `0` if they have the same weight.