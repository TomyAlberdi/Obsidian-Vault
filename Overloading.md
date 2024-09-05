#Development  
Method overloading is related to the [[method signature]]. In [[object-oriented programming]], it is possible to have two or more methods with the same name in the same class, but with different behaviors. This is feasible because when invoking such a method, it can be determined which one to call as long as their signatures differ.
```java
class Dog {
    String name;
    int age;
    void play() {}
    String bark() {}
    void bark(int intensity) {}
}
```
The `bark()` method is overloaded; both methods have different signatures. We can see that one of the `bark()` methods returns a `String`. The name, quantity, type, and order of parameters are part of a method’s signature and must differ to overload it.
The return value of a method and visibility modifiers are not part of the signature. Therefore, overloaded methods can return different things or the same.
### Overriding
When we hear the word "overriding," the first idea that comes to mind is rewriting something that already exists. This idea is very similar to what we find in object-oriented programming and is key to resolving certain scenarios.
To override methods, we need an inheritance relationship, as we are overriding a method from the superclass to make it behave differently in the subclass.
Unlike overloading, where methods must have different signatures, in overriding, the methods must have the same signature.
When writing the `bark()` method in the subclasses, we are indicating that this method is overridden and, therefore, behaves differently.
## Overloading and Overriding in [[Java]]
#### Overloading:
Remember that we can only overload a method if its signature changes.
```java
public double calculateSalary() {
  return salary - deductions;
}

public double calculateSalary(double bonus) {
  return salary - deductions + bonus;
}
```
In this way, when the methods are used, the method whose signature matches the parameters provided will be invoked.
#### Overriding:
The `@Override` keyword indicates that the previous behavior of the method is being overridden. We are rewriting it to solve a problem differently, taking into account the subclass in which we are working.
```java
@Override
public double calculateSalary() {
  return salary - deductions + (salesAmount / 100 * commission);
}
```