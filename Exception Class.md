#Development 
Like all elements in Java, [[exceptions]] are classes and have a certain hierarchy:
![](https://t12904266.p.clickup-attachments.com/t12904266/c23700b6-6c8e-44f7-b8bc-778f70afef84/image.png)
All exceptions inherit from `Exception`, with only some shown in the diagram. Many of the `RuntimeException` exceptions are due to errors made while writing the code. `IOException` exceptions are those that are not dependent on the code.
## Throwing Exceptions
#### protecting Integrity:
When creating a class, we are trying to represent something that has certain behavior. The values stored in its attributes might need to respect a range of values. In this case, we need to protect the integrity of the class.
For example, let’s work with a class that has three attributes for day, month, and year, where days range from 1 to 31, and months range from 1 to 12.
#### Runtime Exception:
```java
public class Date {
  private int day;
  private int month;
  private int year;

  public Date(int d, int m, int y) {
    day = d;
    month = m;
    year = y;
  }
}
```
When using the `Date` class to create a new date, you need to pass three integer values. However, users of a class may not necessarily understand its behavior, so the class should protect itself and prevent invalid values from being set.
```java
public Date(int d, int m, int y) {
  if (d < 1 || d > 31 || m < 1 || m > 12) {
    throw new RuntimeException("Values are not valid");
  }
  day = d;
  month = m;
  year = y;
}
```
By using `throw`, we throw a runtime exception, which we create with the `new` keyword. Now, if we try to create a `Date` instance with invalid values, it will throw an exception.
It is not mandatory to protect `RuntimeException` exceptions with `try` / `catch` blocks.
#### Throwing an Exception:
```java
public Date(int d, int m, int y) throws Exception {
  if (d < 1 || d > 31 || m < 1 || m > 12) {
    throw new Exception("Values are not valid");
  }
  day = d;
  month = m;
  year = y;
}
```
Similarly, we throw the exception with `throw`, but this time it is of type `Exception`, as there isn't a predefined exception for "out of range". We add that we need to notify that the method might throw an exception. This is done after the method signature with the `throws Exception` keywords. This makes it a throwable method.
As it is a throwable method, it must be protected with `try` / `catch`.
```java
public static void main(String[] args) {
  try {
    Date date = new Date(100, -100, 1000);
  }
  catch (Exception e) {
    System.err.println("Invalid values for a date");
  }
}
```