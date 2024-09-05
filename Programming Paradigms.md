#Theory 
A programming paradigm is a way or style of programming [[software]]. There are different ways to design a [[programming language]] and various methods to work to achieve the results programmers need. It is a set of systematic methods at all levels of program design to solve computational problems. Programming languages adopt one or more paradigms depending on the type of commands they allow to implement. These paradigms vary depending on our interests and needs.
### Structured Paradigm:
Follows a line of thought where usually one instruction is executed at a time, and one is governed by a limited set of instructions. This paradigm is widely used for system development. Example: A function `isEven` receives a number and returns "true" if the number is even, and "false" if it is odd.
### [[Object-Oriented Programming|Object-Oriented]] Paradigm:
The code can be grouped in such a way that it represents an entity and interprets messages. The strength of this paradigm lies in using abstractions and creating entities. Example: One piece of code represents a shopping cart. Another piece of code represents a product with its price. Then, I can add the responsibility to the cart to add products and later ask for the total cost.
### Functional Paradigm:
This paradigm is based on a very simple concept, which is mathematical functions. The strength of this paradigm is that whenever function X is given value A, it will always return value B. This property of returning the same value is known as immutability. Example: The functional solution to the problem of whether a number is even or not is very similar to the structured one; we must create a function `isEven` that receives a number and tells us if it is even or odd.
### Logical Paradigm:
Instead of developing steps and instructions, it uses logical rules to query the system, and it infers what to do based on the established logical rules. Example: 
* Logical rules: 
	* Every person whose balance is negative is a debtor. 
	* A 10% interest rate applies to every debtor. 
With this logical set, we could ask, "What is Juan's interest rate?" The system responds by analyzing if Juan is a person, if he is a debtor, and if the interest rate applies to him.
### Domain-Specific Language Paradigm:
The languages found here try to solve very specific problems. Example: When we want to query a supermarket [[database]] to know what products we have in the category of appliances.
### Multiparadigm:
Throughout the evolution of programming, with new challenges and paradigms, there have been languages that have modified their structure to allow solutions in different paradigms. Example: In JavaScript, you can write code using both the structured paradigm and object-oriented programming, and even use the functional paradigm.