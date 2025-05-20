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
### Use Descriptive Names
Don't be afraid to make a name long. A long descriptive name is better than a short enigmatic name. A long descriptive name is better than a long descriptive comment.
Use a naming convention that allows multiple words to be easily read in the function names, and then make use of those multiple words to give the function a name that says what it does.
### Command Query Separation
Functions should either do something or answer something, but not both. Either your function should change the state of an object, or it should return some information about that object. Doing both often leads to confusion.
### Prefer Exceptions to Returning Error Codes
Returning error codes from command functions is a subtle violation of command query separation. It promotes commands being used as expressions in the predicates of `if` statements:
```java
if (deletePage(page) == E_OK)
```
This leads to deeply nested structures. When you return an error code, you create the problem that the caller must deal with the error immediately.
```java
if (deletePage(page) == E_OK) {
	if (registry.deleteReference(page.name) == E_OK) {
		if (configKeys.deleteKey(page.name.makeKey()) == E_OK) {
			logger.log("page deleted)
		} else {
			logger.log("configKey not deleted)
		}
	} else {
		logger.log("deleteReference from registry failed")
	}
} else {
	logger.log("delete failed")
	return E_ERROR;
}
```
On the other hand, if you use exceptions instead of returned error codes, then the error processing code can be separated from the happy path code and can be simplified:
```java
try {
	deletePage(page)
	registry.deleteReference(page.name)
	configKeys.deleteKey(page.name.makeKey())
} catch (Exception e) {
	logger.log(e.getMesage())
}
```
#### Extract `try/catch` Blocks
`try/catch` blocks are ugly in their own right. They confuse the structure of the code and mix error processing with normal processing. So it is better to extract the bodies of the `try` and `catch` blocks out into functions of their own.
```java
public void deletePage(Page page) {
	try {
		deletePageAndAllReferences(page)
	} catch (Exception e) {
		logError(e)
	}
}
private void deletePageAndAllReferences(Page page) throws Exception {
	deletePage(page)
	registry.deleteReference(page.name)
	configKeys.deleteKey(page.name.makeKey())
}
private void logError(Exception e) {
	logger.log(e.getMessage())
}
```
In the above, the `delete` function is all about error processing. It is easy to understand and then ignore. The `deletePageAndAllReferences` function is all about the processes of fully deleting a `page`. Error handling can be ignored. This provides a nice separation that makes the code easier to understand and modify.
==Error Handling is one thing, and functions should do only one thing. Thus, a function that handles errors should do nothing else.==
This implies that, if the keyword `try` exists in a function, it should be the very first word in it, and that there should be nothing after the `catch/finally` blocks.
#### The `Error.java` Dependency Magnet
Returning error codes usually implies that there is some class or enum in which all the error codes are defined.
```java
public enum Error {
	OK,
	INVALID,
	NO_SUCH,
	LOCKED,
	OUT_OF_RESOURCES,
	WAITING_FOR_EVENT
}
```
Classes like this are a *dependency magnet*; many other classes must import and use them. Thus, when the `Error` enum changes, all those other classes need to be recompiled and redeployed.
When you use exceptions rather than error codes, then new exceptions are *derivatives* of the exception class. They can be added without forcing any recompilation or redeployment.
### Don't Repeat Yourself
Duplication is a problem because it bloats the code and will require *n*-fold modification should an algorithm ever have to change. It is also a *n*-fold opportunity for an error of omission.
Consider how object-oriented programming serves to concentrate code into base classes that would otherwise be redundant. Structured programming, Aspect Oriented Programming, Component Oriented Programming are all, in part, strategies for eliminating duplication.