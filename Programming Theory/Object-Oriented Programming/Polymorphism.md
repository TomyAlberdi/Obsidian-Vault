Created: 2024-09-17 17:11
## Family Tree:
1. Computer
2. Programming Theory
3. [[Object-Oriented Programming]]
-- -
Polymorphism is the ability of an object to behave as another. In other words, it is the capacity of an object to function in various forms. Let’s look at the previous examples:
Example:
```java
Dog p;

p = new Doberman();
p.bark();

p = new Poodle();
p.bark();
```
The reference `p` can behave and bark like a `Doberman`. The same reference `p`, when dynamically bound (Dynamic Binding) to a `Poodle`, behaves and barks like a `Poodle`.
By using polymorphism, we can be confident that future modifications adding new subclasses should not affect the code or its functionality. If the code uses `Dog` (that is, any object that "is a" `Dog`), as long as new dog breeds introduced into the system inherit from `Dog`, they will work correctly.
### Casting:
Suppose `Doberman` has a method called `biteLikeDoberman()`, but the reference, i.e., the variable, is of type `Dog`. To force a dog to be treated as a `Doberman`, we use casting. This allows us to invoke methods specific to `Doberman`.
```java
Dog dog = new Doberman();
dog.bark();

((Doberman)dog).biteLikeDoberman();
```
The same applies if our object reference is of type `Object`. In this case, since the `Object` class does not have the `bark()` method, we must cast it to either `Dog` or `Doberman`.
Example:
```java
Object dog = new Doberman();

((Dog)dog).bark();

((Doberman)dog).biteLikeDoberman();
```