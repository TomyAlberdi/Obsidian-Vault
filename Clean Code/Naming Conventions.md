Created: 2025-05-07 20:26
## Family Tree:
1. [[Clean Code]]
-- -
### Introduction
The hardest thing about choosing good names is that it requires good descriptive skills and a shared cultural background. This is a teaching issue rather than a technical, business or management issue. As a result, many people in this field don't learn to do it very well.
People are also agraid of renaming things for fear that some other developers will object. We do not share that fear and find that we are actually grateful when names change for the better.
Most of the time we don't really memorize the names of classes and methods. We use the modern tools to deal with details like that so we can focus on whether the code reads like paragraphs and sentences, or at least like tables and data structure (a sentence isn't always the best way to display data). 
### Use Intention-Revealing Names
The name of a variable, function, or class should answer the next questions:
- Why it exists.
- What it does.
- How it is used.
==If a name requires a comment, then the name does not reveal its intent.==
### Avoid Disinformation
Spelling similar concepts similarly is *information*. Using incosistent spellings is *disinformation*.
### Make Meaningful Distinctions
Programmers create problems for themselves when they write code solelu to satisfy a compiler or interpreter. For example, because you can't use the same name to refer to different things in the same scope, you might be tempted to change one name in an arbitrary way.
It is not sufficient to add number series or noise words, even though the compiler is satisfied. If names must be different, then they should also mean something different.
- Number-series naming (*a1, a2, ..., aN*) is the opposite of intentional naming.
- Noise words are redundant (The word `variable` should never appear in a variable name)
### Use Searchable Names
Single-letter names and numeric constants have a perticular problem in that they are not easy to locate across a body of text.
Single-letter names can **only** be used as local variables inside short methods.
==The length of a name should correspond to the size of its scope.==
### Avoid Mental Mapping
Readers shouldn't have to mentally translate your names into other names they already know. This problem generaly arises from a choice to use neither problem domain terms nor solution domain terms.
This is a problem with single-letter names. Single-letter names for loop counters are traditional. However, in most other contexts it's just a placeholder that the reader must mentally map to the actual concept.
### Class Names
Class and objects should have noun or noun phrase names like `Customer`, `Account` and `AddressParser`. Avoid words like `Manager`, `Processor`, `Data` or `Info` in the name of a class. A class name should not be a verb.
### Method Names
Method names should have verb or verb phrase names like `postPayment`, `deletePage` or `save`. Accessors, mutuators and predicates should be named for their value and prefixed with `get`, `set`, and `is` according to the javabean standard. For example:
```java
string name = employee.getName();
customer.setName('Mike');
if (paycheck.isPosted()) { ... }
```
When constructors are overloaded, use static factory methods with names that describe the arguments. For example:
```java
Complex fulcrumPoint = Complex.FromRealNumber(23.0);
```
Is generaly better than:
```java
Complex fulcrumPoint = new Complex(23.0)
```
Consider enforcing their use by making the corresponding constructors private.
### Don't Be Cute
Cureness in code often appears in the form of colloquialisms or slang. For example, don't use the name `whack()` to mean `kill()`. Don't tell little culture-dependent or personal sense of humor-dependent jokes.
### Pick One Word per Concept
Pick one word for one abstract concept and stick with it. For instance, it's confusing to have `fetch`, `retrieve`, and `get` as equivalent methods of different classes. The function names have to stand alone, and they have to be consistent in order for you to pick the correct method without any additional exploration.
### Use Solution Domain Names
The people who read your code will also be programmers, so go ahead and use computer science terms, algorithm names, pattern names, math terms, etc.
### Don't Add Gratuitous Context
Shorter names are generally better than longer ones, so long as they are clear. Add no more context to a name than is necessary.
The names `accountAddress` and `customerAddress` are fine names for instances of the class `Address`, but could be poor names for classes.
`Address` is a fine name for a class, but if I need to differentiate between MAC addresses, por addresses and Web addresses, I might consider renaming it to `PostalAddress`. The resulting name is more precise, which is the point of all naming.