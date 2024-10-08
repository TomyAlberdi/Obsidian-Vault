Created: 2024-09-17 17:10
## Family Tree:
1. Computer
2. Programming Theory
3. [[Object-Oriented Programming]]
-- -
In general terms, a signature allows us to identify ourselves and express our consent to a particular document. In our identity document, we can find many elements, including the signature or rubric. With this idea, we will address the signature of a method in Object-Oriented Programming, which is nothing more than the complete definition of a method, that is, its name, its parameters, their types, and the order of appearance of these parameters. In the same class, there cannot be two methods with the same signature, that is, with the same name and number of parameters with their respective types in the same order. We say, then, that the following methods have different signatures; they are different methods because, although they have the same name, they have a different number of parameters or differ in some of their types:
- `add(number1: Double, number2: Double): Double`
- `add(number1: Double, number2: Double, number3: Double): Double`
- `add(number1: Integer, number2: Integer): Integer`