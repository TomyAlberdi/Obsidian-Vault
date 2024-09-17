Created: 2024-09-17 17:28
## Family Tree:
1. Computer
2. Programming Theory
3. Object-Oriented Programming
4. [[Design Patterns]]
-- -
Composite is a pattern that falls within the structural (Design Patterns > Structural Patterns) category. It focuses on how objects are composed to form composite structures.
- **Client**: The client interacts with all elements through the component interface. As a result, the client can work with any of the elements in the same manner.
- **Component Interface (Development/Backend Development/Java/Interfaces)**: The component interface defines the common operations for both simple and complex elements of the tree.
- **Leaf**: The leaf is a basic element of a tree that has no sub-elements. Typically, leaf components end up doing much of the actual work, as they have no one else to delegate it to.
- **Composite**: The container (or composite) is the element that contains sub-elements, either leaves or other containers. A container does not know the concrete class of its children; it works with all sub-elements through the component interface.
## Example:
Assuming we want to build a hierarchical structure of departments within a company. Let's look at the following UML diagram:
![](https://t12904266.p.clickup-attachments.com/t12904266/595191a5-0d6d-4392-979f-99d5ea5ee076/image.png)
#### Interface `Departamento`:
```java
public interface Departamento {
  void getName();
}
```
For the leaf components, we will define classes for the Finance and Sales departments:
#### `Finance Department` class:
```java
public class DepartFinanciero implements Departamento {
  private int id;
  private String name;
  
  public void getName() {
    return getClass().getSimpleName();
  }
}
```
#### `Sales Department` class:
```java
public class DepartVentas implements Departamento {
  private int id;
  private String name;
  
  public void getName() {
    return getClass().getSimpleName();
  }
}
```
#### `Composite Department` class:
This is a composite class that contains a collection of `Departamento` class components and also methods to add or remove elements from this collection. The composite `getName()` method is implemented by iterating over the list of leaf elements and invoking the appropriate method for each one.
```java
public class DepartComposite implements Departamento {
  private int id;
  private String name;
  private ArrayList<Departamento> childDepartments;

  public DepartComposite(int id, String name) {
    this.id = id;
    this.name = name;
    this.childDepartments = new ArrayList<>();
  }
  
  public void getName() {
    childDepartments.forEach(Departamento::getName);
  }
  
  public void addDepart(Departamento departamento) {
    childDepartments.add(departamento);
  }
  
  public void removeDepart(Departamento departamento) {
    childDepartments.remove(departamento);
  }
}
```