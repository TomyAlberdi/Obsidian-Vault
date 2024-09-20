Created: 2024-09-20 13:10
## Family Tree:
1. Computer
2. Frontend Development
3. [[JavaScript]]
-- -
## Variables
A variable is a memory space where data is stored and can be reused in the future. In JavaScript, variables are created using reserved keywords. Variable names cannot include accents, spaces, and should not start with an uppercase letter. JavaScript is a case-sensitive language, meaning it distinguishes between uppercase and lowercase letters. To assign a value to a variable, the assignment operator, or equal sign (=), is used. Example of variable creation:
```js
let number = 1234;
```
- `let`: Reserved keyword.
- `number`: Name of the variable.
- `1234`: Value of the variable.
Once a variable has been declared, its value can be modified:
```js
number = 5678;
```
Reserved keywords for creating variables:
- `let`: A variable declared with the `let` keyword cannot be redefined within the same block of code.
- `const`: A variable declared with the `const` keyword is called a constant and cannot have its value changed in any way once assigned. It's common to write constant names in uppercase.
- `var`: Although no longer used, variables declared with `var` have global scope, meaning they can be modified anywhere in the code.
Both `let` and `const` create variables that can only be accessed from the block of code in which they are declared, meaning they do not have global scope.
The reserved keywords `let`, `var`, and `const` can only be used for their intended purpose. They cannot be used as variable names, function names, methods, or object identifiers.
### Data Types:
JavaScript handles two main types of data: primitive data and complex or composite data. Primitive data types are the most important when learning to program in JavaScript:
- **Number**: Represents an integer or decimal number. Example: `let num = 12;`.
- **String**: Alphanumeric text of any length. When declared, double or single quotes are used to delimit the content. Example: `let text = "Hello, world";`.
- **Boolean**: Stores only two types of values: `true` or `false`. No quotes are used in its declaration, as doing so would turn the variable into a string. Example: `let boolean = true;`.
Other relevant data types:
- **Undefined**: Indicates the absence of a value. Variables have an undefined value until one is assigned.
- **Null**: Assigned by the programmer to indicate an empty or unknown value.
- **NaN**: The global `NaN` property is a numeric value that represents "Not-a-Number," indicating that the assigned value is not a number. It results from failed or impossible mathematical operations.
### Literal Object:
Used to place multiple data types in a single variable, which can be accessed independently. To create a literal object, curly braces are used, and within them, a key is followed by a colon and a value, which can be of any type. To add more keys and values, a comma is placed at the end of each line.
```js
let literalObject = {
  key: value,
  key: value2,
};
```
### Array:
Also called a list or array, it allows grouping multiple data types into a single variable, but it differs in that it doesn't have keys, as it uses numeric indexes that start from 0. To create an array, brackets are used after the assignment operator.
```js
let newArray = ["data1", "data2", "data3"];
```
## Operators
Operators allow us to manipulate variable values, perform operations, and compare their values.
#### Assignment: 
It uses the equal sign ( = ) and allows us to assign a value to a specific variable:
```js
let name = "Tomás"
```
#### Arithmetic:
Perform mathematical operations and return the result.
- **Basic**: Addition `1+1=2`, subtraction `1-1=0`, multiplication `2*2=4`, division `4/2=2`.
- **Increment**: Increases a value by 1. Example: `15++ = 16`.
- **Decrement**: Decreases a value by 1. Example: `15-- = 14`.
- **Modulus**: Returns the remainder of a division. Example: `15 % 4 = 3`.
#### Concatenation:
Used to join strings. They return the resulting string. Example: `'hello' + ', world' = 'hello, world'`.
#### Comparison:
Compares two values and returns true or false.
- **Basic**: Greater than `2>1 = true`, less than `1<2 = true`, greater than or equal to `5>=5 = true`, less than or equal to `2<=2 = true`.
- **Simple** comparison: Compares only the values. Example: `10 == 15 = false`, `4 != 2 = true`.
- **Strict comparison**: Compares values and data types. Example: `10 === '10' = false` (different data types), `10 !== 15 = true`.
#### Logical:
These allow you to check boolean values, and the result also returns a boolean. There are three logical operators:
- **And operator**: Verifies if both values are true. Example: `fifteen==15 && ten==10`.
- **Or operator**: Verifies if one or both values are true. Example: `fifteen==15 || ten==9`.
- **Negation operator**: Changes a boolean value to its opposite.
## Functions
A function is a block of code that allows us to group functionality for reuse whenever needed. It typically performs a specific task and returns a value as a result. For the function to execute, "something" must invoke it. It's a very useful tool because it makes the code cleaner and more scalable.
### Types of functions:
#### Declared Functions: 
These are functions that receive a formal name and are not assigned as a value to a variable:
```js
function sum() {...}
```
They are loaded before any code is executed.
#### Expressed Functions:
These are functions that are assigned as a value to a variable:
```js
let sum = function() {...}
```
They are only loaded when the interpreter reaches the line of code where the function is located.
#### Arrow Functions:
There is a more compact way to create or express our functions. Arrow functions are a way to create functions introduced in **ES6 (ECMAScript version 6)**. One of their advantages is that they are more concise than traditional functions created with the `function` keyword.
For example:
* Declared function:
```js
function sum(a, b) {
  return a + b;
}
console.log(sum(2, 4));
```
- Arrow function:
```js
let sum = (a, b) => a + b;
console.log(sum(2, 4));
```
Note that if the function contains more than one line of code, you need to use curly braces:
```js
let isMult = (a, b) => {
  let rest = a % b;
  return rest == 0;
}
```
## Control Structures
To make decisions when writing code, control flow mechanisms, also called **conditionals**, are used. These allow us to evaluate conditions and take different actions depending on the result of the evaluation.
### `IF`:
The most basic version of `if` sets a condition and a block of code to execute if the condition is met.
```js
if (condition) {
  // Code to execute if the condition is true
}
```
### `IF ELSE`:
Similar to the previous example, but adds a block of code to execute if the condition is false. It's important to note that the `else` block is optional.
```js
if (condition) {
  // Code to execute if the condition is true
} else {
  // Code to execute if the condition is false
}
```
### `ELSE IF`:
Similar to the previous example, but it adds an additional `if`. This means another condition that can be evaluated if the first one is false. You can add as many `else if` blocks as needed, but only one of them can be true. If none are true, the `else` block will be executed, if it exists.
```js
if (condition) {
  // Code to execute if the condition is true
} else if (another condition) {
  // Code to execute if the other condition is true
} else {
  // Code to execute if all conditions are false
}
```
### Ternary `IF`:
Unlike the traditional `if`, the **ternary if** does not use the `if` or `else` keywords, nor the curly braces to enclose the block of code to be executed. It is written entirely in a horizontal format:
```js
condition ? expression for true : expression for false;
```
It is mandatory to include the code to be executed when the condition is not met. If nothing should happen in that case, an empty string can be used. The result of the ternary `if` is often stored in a variable:
```js
let greater = 4 > 10 ? "4 is greater" : "10 is greater";
```
### Switch:
The **switch** structure works similarly to `if`, with the particularity that you can establish code blocks for any case related to the set condition:
```js
switch (condition) {
  case case1:
    console.log("Case 1 is met");
    break;
  case case2:
    console.log("Case 2 is met");
    break;
  default:
    console.log("None of the cases are met");
    break;
}
```
## Repetition Structures
**Loops** allow us to repeat instructions easily. We can either repeat them a specific number of times or as long as a condition is met.
### `For` loop:
It consists of 3 parts defined within parentheses. Together, they allow us to determine how the repetitions will be carried out and define the instructions we want to execute in each iteration.
```js
for (start; condition; modifier) {
  // Code to execute
}
```
**Example:** Use a For Loop to count from 1 to 5, inclusive.
```js
for (let loop = 1; loop <= 5; loop++) {
  console.log('On round number ' + loop);
}
```
- `let loop = 1`: Sets the name and initial value of the counter.
- `loop <= 5`: Before executing the code in each iteration, it checks if the condition is true or false. If true, it executes the code; if false, it stops the loop.
- `loop++`: After executing the code, the counter is updated as specified. In this case, 1 is added, but we can perform any operation we want.
In each cycle, it checks if the value of `loop` is less than or equal to 5. If so, it executes `console.log()` and increments the value of `loop` by 1. When `loop` is no longer less than or equal to 5, the loop stops.
### `While` loop:
**While Loop** It has a structure similar to `if/else` conditionals: a reserved keyword + condition in parentheses. However, the while loop repeatedly evaluates the condition and executes its block of code until the condition is no longer true.
```js
while (condition) {
  // Code to execute while the condition is true
}
```
**Example:** (same as the For Loop example)
```js
let loop = 1;
while (loop <= 5) {
  console.log('On round number ' + loop);
  loop++;
}
```
Before executing the code, it checks if the condition is true or false. If true, it continues with the instructions; if false, the loop stops.
It's important to create the counter at the start to avoid what's known as an **infinite loop**. An infinite loop occurs when the condition is always true, causing the code to run endlessly. This can lead to several issues, the most significant being the program crashing.
### `Do While` Loop:
Unlike the while loop, in the Do While loop, the condition is checked after the block of code has been executed. Therefore, regardless of the result, the actions will be performed at least once.
```js
let loop = 5;
do {
  console.log('On round number ' + loop);
  loop++;
} while (loop <= 5);
```
Other than this, the Do While loop is identical to the while loop.