Created: 2024-09-17 15:43
## Family Tree:
1. Computer
2. Backend Development
3. [[Java]]
-- -
When an error occurs in your Java code due to an exceptional situation, the way to handle it is by using exceptions. To use exceptions, you have `try` / `catch` blocks.
#### Example:
If you have a generic program that asks the user for two numbers and returns the result of dividing one by the other, if the user enters 0 as the divisor, you will get the following error in the form of an exception:
```powershell
Exception in thread "main" java.lang.ArithmeticException: / by zero
  at com.company.Main.main(Main.java:16)
```
#### Solution:
```java
try {
  division = num1 / num2;
  System.out.println(division);
}
catch (ArithmeticException exception) {
  System.err.println("Attempted to divide by zero");
}
```
* In the `try` block, you place the instructions that might cause a problem, in this case, the division if the divisor is 0.
* The `catch` block "catches" the exception. If a division by zero occurs, that exception is caught and, in this case, an error message is displayed with `System.err.println()`. If a division is performed without issues, the `catch` block does not execute.
`ArithmeticException` is the type of exception that occurred. When it happens, an object, in this case, `exception`, is created.
### Multiple Catch Blocks:
The `try` / `catch` blocks allow you to use more than one `catch`. This way, you can handle specific exceptions first and then handle more general ones.
### Finally:
You can add a `finally` block to the `try` / `catch` structure, which is optional. The `finally` block is always executed. If an exception occurs and is caught by a `catch` block, the `finally` block will still execute.
```java
try {
  // Code that may throw an exception
}
catch (SpecificException ex) {
  // Handling of specific exception
}
finally {
  // Code that will always execute
}
```