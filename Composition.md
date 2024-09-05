#Theory 
Composition is a type of [[aggregation]] that is stronger, where all parts (classes) can only belong to a whole and we represent it as a filled diamond instead of an empty one as in aggregation. It is the case where an [[object class]] A "owns" an object class B, and B has no reason to exist without A. As mentioned earlier, unlike aggregation, in this case, the part has no meaning without the whole. Example:
A company has employees; these employees do not make sense on their own. If an employee exists, it is because there must be a company where that employee works.

In composition, instead of statically encoding behavior as is done with [[inheritance]], we define small, predefined behaviors and use them to declare more complex behaviors. For example:
```java
public class Sistema {
  Persona persona = new Persona();
}
public class Persona {}
```
### Advantages and disadvantages:
##### Advantages:
- The behavior can be chosen at runtime instead of being bound at compile time.
- Objects that were instantiated and are contained within the class that instantiates them are only accessed through their interface, thus adhering to the principle of programming to an interface rather than an implementation.
##### Disadvantages:
- The software is highly dynamic and parameterized, making it more difficult to understand than static software.
### Usage:
In general, composition is always preferred over inheritance. However, we can define some rules to identify when inheritance can be used to avoid the problems it entails:
- Inheritance is used if an instance of a child class will never need to become an object of another class.
- If the inheritance hierarchy represents an "Is a" relationship rather than a "Has a" relationship.
- If you want or need to make global changes to your subclasses by changing a parent class.
- When the subclass extends rather than entirely or partially replaces the responsibilities of the parent class.