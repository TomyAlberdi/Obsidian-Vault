Let's see how we can solve problems when we are not sure which object should handle a specific request.
## Purpose
It is a [[Design Patterns#Behavioral Patterns|behavioral]] design pattern that allows requests to be passed along a chain of handlers (drivers). Upon receiving a request, each handler decides whether to process it or pass it to the next driver in the chain.
## Solution
Create a chain with driver classes to process the client's request. Each one has a field to store a reference to the next driver in the chain. The request travels through the chain until all the drivers have had the opportunity to process it (the drivers can decide not to pass the request and stop the procedure).
![[image 10.png]]
## Advantages
- Greater flexibility in processing client requests. It is possible to add objects that can handle new responsibilities or modify existing ones without affecting the client.
- Reduced coupling: It allows an object to send a request knowing it will be handled, but neither the sender nor the receiver knows anything about each other.
## Disadvantages
- Implementing the chain can be complex, and if not well configured, some requests may not be handled properly.
## Implementation
We will create an [[abstract class]] responsible for storing a reference to the next driver in the chain and a method to send the client's request to it. Concrete drivers can use this behavior by invoking the parent method.  
One by one, we create concrete driver subclasses and implement the methods. Each driver must make two decisions when receiving a request:
1. Whether to process the request.
2. Whether to pass the request to the next driver in the chain.
The client can activate any driver in the chain, not just the first one. The request will be passed along the chain until a driver refuses to pass it further or until it reaches the end. Due to the dynamic nature of the chain, the client must be prepared to handle the following scenarios:
- The chain may consist of a single link.
- Some requests may not reach the end of the chain.
- Others may reach the end of the chain without being handled.
## Example
Let's imagine we're developing a system for the credit department of a bank, and we want that when a client requests a loan, the request is sent to different individuals responsible for approving it. The bank has indicated the following:
- If the amount is less than 60,000, the account executive can approve it.
- If the amount is between 60,000 and 200,000, the manager is responsible for approving it.
- If the amount is greater than 200,000, the director must approve it.
### Implementation
The **`driver`** class is responsible for starting the chain. In this case, the `EmpleadoBanco` class is as follows:
```java
public abstract class BankEmployee {

   private BankEmployee nextBankEmployee;

   public abstract void processRequest(Integer amount);

   public void setNextBankEmployee(BankEmployee emp) {
       nextBankEmployee = emp;
   }

   public BankEmployee getNextBankEmployee() {
       return nextBankEmployee;
   }
}
```
### Subclasses:
Here, we define the criteria and how each class processes the request:
```java
public class AccountExecutive extends BankEmployee {
   @Override
   public void processRequest(Integer amount) {
       if (amount < 60000)
           System.out.println("I'll take care of it. Account Executive.");
       else if (getNextBankEmployee() != null)
           getNextBankEmployee().processRequest(amount);
   }
}
public class Manager extends BankEmployee {
   @Override
   public void processRequest(Integer amount) {
       if (amount >= 60000 && amount <= 200000)
           System.out.println("I'll take care of it. Manager.");
       else if (getNextBankEmployee() != null)
           getNextBankEmployee().processRequest(amount);
   }
}
public class Director extends BankEmployee {
   @Override
   public void processRequest(Integer amount) {
       if (amount > 200000)
           System.out.println("I'll take care of it. Director.");
       else if (getNextBankEmployee() != null)
           getNextBankEmployee().processRequest(amount);
   }
}
```
### Main Class:
In the `Main` class, we set up the chain of responsibility and test the process with a loan request:
```java
public class Main {
   public static void main(String[] args) {

       BankEmployee employee1 = new AccountExecutive(); 
       BankEmployee employee2 = new Manager();
       BankEmployee employee3 = new Director();
    
       employee2.setNextBankEmployee(employee3);
       employee1.setNextBankEmployee(employee2); 

       employee1.processRequest(78000);  // Example request for 78,000
   }
}
```
### Explanation:
- The `BankEmployee` class defines the basic structure for the chain, holding a reference to the next employee (`nextBankEmployee`) and an abstract method `processRequest` that each subclass must implement.
- The subclasses (`AccountExecutive`, `Manager`, and `Director`) each handle the request based on the amount. If they can't handle it, they pass it to the next employee in the chain.
- In the `Main` class, we link the chain by setting each employee's successor using `setNextBankEmployee` and then initiate the request processing with `employee1.processRequest(78000);`.
With this setup, a request for 78,000 will be passed from the account executive to the manager, who will then handle it.