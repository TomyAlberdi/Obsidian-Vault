Created: 2025-05-17 00:16
## Family Tree:
1.  Clean Code
2. [[Functions]]
-- -
The ideal number of arguments for a function is zero (**niladic**). Next comes one (**monadic**), followed closely by two (**dyladic**). Three arguments (**triadic**) should be avoided where possible. More than three (**polyadic**) requires very special justification -and then shouldn't be used anyway.
Arguments are harder from a testing point of view. Imagine the difficulty of writing all the test cases to ensure that all the various combinations of arguments work properly. If there are no arguments, this is trivial.
### Common Monadic Forms
There are two very common reasons to pass a single argument into a function. You may be asking a question about that argument, or you may be operating on that argument, transforming it into something else and *returning it*.
These two uses are that readers expect when they see a function. You should choose names that make the distinction clear, and always use the two forms in a consistent context.
A somewhat less common, but still very useful form for a single argument function, is an *event*. In this form there is an input argument but no output argument. The overall program is meant to interpret the function call as an event and use the argument to alter the state of the system. Use this form with care, it should be very clear to the reader that this is an event. Choose names and contexts carefully.
Try to avoid any monadic functions that don't follow these forms. Using an output argument instead of a return value for a transformation is confusing. If a function is going to transform its input argument, the transformation should appear as the return value.
### Flag Arguments
Passing a boolean into a function is a truly terrible practice. It immediately complicates the signature of the method, proclaming that this function does more than one thing, because is does one thing if the flag is true and another if the flag is false.
### Argument Objects
When a function seems to need more than two or three arguments, it is likely that some of those arguments ought to be wrapped into a class of their own. Consider the difference between the two following declarations:
```java
Circle makeCircle(double x, double y, double radius);
Circle makeCircle(Point center, double radius);
```
When groups of variables are passed together, the way *x* and *y* are in the example above, they are likely part of a concept that deserves a name of its own.
### Argument Lists
Sometimes we want to pass a variable number of arguments into a function. Consider the `String.form` method:
```java
String.format("%s worked %.2f hours.", name, hours);
```
If the variable arguments are all treated identically, as they are in the example above, then they are equivalent to a single argument of type `List`. By that reason, `String.format` is actually dyadic:
```java
public String format(String format, Object... args)
```
### Verbs and Keywords
Choosing good names for a function can go a long way toward explaining the intent of the function and the order and intent of the arguments.
In the case of a monad, the function and argument should forma very nice verb/noun pair. For example, `write(name)` is very evocative. An even better name might be `writeField(name)`, which tells us that the "name" thing is a field.
This last is an example of the *keyword* form of a function name. Using this form we encode the names of the arguments into the function name. For example, `assertEquals` might be better written as `assertExpectedEqualsActual(expected, actual)`. This strongly mititgates the problem of having to remember the ordering of the arguments.
### Output Arguments
Arguments are most naturally interpreted as *inputs* to a function. In the days before OOP it was sometimes necessary to have output arguments. However, much of the need for output arguments disappears in OO languages because `this` is *intended* to act as an output argument. In other words, output arguments should be avoided. If your function must change the state of something, have it change the state of its owning object.