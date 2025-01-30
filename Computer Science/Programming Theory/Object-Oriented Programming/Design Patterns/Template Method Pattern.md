Created: 2024-09-17 17:34
## Family Tree:
1. Computer
2. Programming Theory
3. Object-Oriented Programming
4. [[Computer Science/Programming Theory/Object-Oriented Programming/Design Patterns/Design Patterns]]
-- -
Let's imagine that in our system several classes do the same thing but have some different details. Could it be that we have repeated code among these classes?
## Purpose
It is a behavioral (Design Patterns > Behavioral Patterns) design pattern that defines the skeleton of an algorithm in the superclass but allows subclasses to override certain steps of the algorithm without changing its structure.
## Solution
The skeleton method consists of the code that these classes have in common, allowing some parts to be modified by the subclass that implements it, thus placing the repeated code in one place.
![[Computer Science/Programming Theory/Object-Oriented Programming/Design Patterns/attachments/image 9.png]]
## Advantages
- Clients can override certain parts of a large algorithm, making them less affected by changes in other parts of the algorithm.
- Duplicated code can be placed within a superclass.
## Disadvantages
- "Skeleton" methods tend to be harder to maintain as the number of steps to implement increases.
- Some clients may be limited by the skeleton provided by the algorithm.
## Implementation
1. We consider which steps are common to all subclasses where we see repeated code and which will always be unique to each one.  
2. We create an abstract class and declare the skeleton method and a set of abstract methods that represent the steps of the algorithm to be implemented by the subclasses.  
3. For each variation of the method, we create a new concrete subclass. This subclass must implement all the defined abstract steps.
## Example
Let's look at an example of the template method pattern using an analogy from real life. Think of a pizzeria and the process of preparing different types of pizzas. Let's try to identify the steps a cook must take to prepare and deliver a pizza. They could be:
- Prepare the dough.
- Precook the dough.
- Prepare the ingredients.
- Add the ingredients.
- Cook the pizza.
- Package the pizza.
For each variety of pizza, cooks have to go through all of these steps. By applying the template method pattern, we could create the skeleton method with the steps common to all pizzas, and let the cooks only focus on the unique steps for each pizza, in this case, preparing and adding the ingredients. Let's see how we represent this solution in a UML diagram:
### Implementation:
Code for the abstract class that defines the skeleton method and the abstract methods to be implemented by the subclasses.
```java
public abstract class Cook {

   public void makePizza(){
       prepareDough();
       precookDough();
       prepareIngredients();
       addIngredients();
       cookPizza();
       packagePizza();
   }

   protected abstract void prepareIngredients();
   protected abstract void addIngredients();

   private void prepareDough(){
       System.out.println("Preparing dough..");
   }

   private void precookDough(){
       System.out.println("Precooking dough..");
   }

   private void cookPizza(){
       System.out.println("Putting pizza in the oven");
   }

   private void packagePizza(){
       System.out.println("Packaging pizza");
   }
}
```
Code for the subclass `NonVeggieCook`:
```java
public class NonVeggieCook extends Cook {
   @Override
   protected void prepareIngredients() {
       System.out.println("Preparing cheese and ham,");
   }

   @Override
   protected void addIngredients() {
       System.out.println("Adding ingredients");
   }
}
```
Code for the subclass `VeggieCook`:
```java
public class VeggieCook extends Cook {

   @Override
   protected void prepareIngredients() {
       System.out.println("Preparing tomatoes and cheese");
   }

   @Override
   protected void addIngredients() {
       System.out.println("Adding cheese and tomatoes");
   }
}
```
Code for the `Main` class:
```java
public class Main {

   public static void main(String[] args) {
       Cook veggieCook = new VeggieCook();
       Cook nonVeggieCook = new NonVeggieCook();

       veggieCook.makePizza();
       nonVeggieCook.makePizza();
   }
}
```