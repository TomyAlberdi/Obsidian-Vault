#Development 
There will be times when we need to model classes that are incomplete, meaning they are only fully implemented in the subclasses, where the specific implementation takes place. We call these abstract classes.
Abstract classes are those that cannot be identified with something concrete on their own (they don't exist as such in the real world) but possess certain characteristics that are common to other classes that will [[Inheritance|inherit]] from them.
These classes allow us to declare methods that are not implemented, meaning they do nothing in the abstract class. These methods, which we also call abstract methods, require the subclasses to [[Overloading#Overriding|override]] them in order to provide an implementation.
### Model:
In UML diagrams, abstract classes can be represented either by writing their name in italics or by explicitly indicating `<<abstract>>` above their name. We can choose either option.
On the other hand, abstract methods are represented by prefixing the word `abstract` to the method name.
Example:
```java
abstract class Dog {
    String name;
    int age;
    void play() {}
    abstract void bark();
}
```
In this way, an abstract class can have attributes and methods that will be inherited by subclasses, as well as abstract methods that force the subclasses to override them for implementation.
## Abstract classes in [[Java]]
We define abstract classes and their behavior using the `abstract` keyword. Since the behavior is abstract (we only specify _what_ to do), abstract methods have no associated code or "body."
Example:
```java
public abstract class Dog {
  public abstract String bark();
}
```
The rules for implementing abstract methods are the same as those for overriding methods, so the same rules apply: respect the type, quantity, and order of parameters.