#Cheatsheet 
Singleton is a [[Design Patterns#Creation Patterns|creational design pattern]] that ensures a class has only one instance and provides a global access point to it. In the Singleton pattern, a class manages its own instance and prevents any other class from creating an instance of it. To create the instance using this pattern, you must go through the class itself, as no other class can instantiate it. The Singleton pattern also provides a global access point to its instance. The class will always offer its own instance, and if it doesn't have one yet, it creates and returns that newly created instance.
### Creating a Class
To create a class with this pattern, the following steps are necessary:
1. Create a static attribute of the same type as the class with the name `instance`.
2. All constructors of the class must use the `private` modifier.
3. Create a static `getInstance()` method that returns the `instance` attribute.
```java
public class SingletonExample {
  // Attribute with the same name as the class
  private static SingletonExample instance = new SingletonExample();
  // Private constructor
  private SingletonExample() {}
  // Static method
  public static SingletonExample getInstance() { return instance; }
}
```
This pattern is used when a single point of instantiation for a class is needed.
### Lazy Initialization:
This implementation technique of the Singleton pattern states that until the `getInstance()` method is invoked, no object is created in memory.
```java
public static Class getInstance() {
  if (instance == null) {
    instance = new Class();
  }
  return instance;
}

```
## Example:
Typically, a class that does not need more than one instance is the class used for [[database]] connection. We are aware of the potential issues that can arise from having more than one connection to a database within the same execution of code. To avoid these issues, we must block even the slightest possibility of instantiating this class outside of itself (even subclasses cannot instantiate it) and also create a way to ensure that only one instance of it exists. In this context, the best solution is to apply the Singleton pattern.
```java
public class Database {
  private static Database instance = new Database();
  // Private constructor to prevent instantiation
  private Database() {
    // Initializations
  }
  // Static method to get the single instance
  public static Database getInstance() { 
    return instance; 
  }
}
```
In this example, the `Database` class is designed so that only one instance can exist, and this instance is accessed globally via the `getInstance()` method. This implementation ensures that no other instance of the `Database` class can be created, thus preventing potential issues with multiple database connections.