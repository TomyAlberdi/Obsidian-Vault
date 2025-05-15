Created: 2025-05-08 19:03
## Family Tree:
1. [[Clean Code]]
-- -
### Blocks and Indenting
The blocks within `if`, `else`, `while`, etc; statements should be one line long. Probably that line should be a function call. Not only does this keep the enclosing function small, but it also adds documentary value because the function called within the block can have a nicely descriptive name.
This also implies that functions should not be large enough to hold nested structures. Therefore, the indent level of a function should not be greater than one or two.
This makes the functions easier to read and understand.
### Do One Thing
==Functions should do one thing. They should do it well. They should do it only.==
The problem with this statement is that it is hard to know what "one thing" is. If a function does only those steps that are one level below the stated name of the function, then the function is doing one thing. After all, the reason we write functions is to decompose a larger concept into a set of steps at the next level of abstraction.
Another way to know if a function is doing more than "one thing", is if you can extract another function from it with a name that is not merely a restatement of its implementation.
#### One Level of Abstraction per Function
In order to make sure our functions are doing "one thing", we need to make sure that the statements within our function are all at the same level of abstraction.
Mixing levels of abstraction within a function is always confusing. Readers may not be able to tell whether a particular expression is an essential concept or a detail.
### *The Stepdown Rule*
We want the code to read like a top-down narrative. Every function has to be followed by those at the next level of abstraction so that we can read the program descending one level of abstraction at a timer as we read down the list of functions.
