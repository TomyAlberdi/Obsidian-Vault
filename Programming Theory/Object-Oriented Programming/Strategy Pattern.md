A certain object might have behavior that is initially simple and consistent, but at times, this behavior can become more complex and may need to change based on specific requirements. The Strategy [[Design Patterns|pattern]] allows algorithms to vary independently of the client using them. It offers a straightforward solution based on an object that can change, with its behavior adapting to different circumstances.
### Solution:
The pattern introduces a `Strategy` interface, which defines the method signatures that will change. Different classes implement this `Strategy` interface, known as `ConcreteStrategy`, and each of these classes contains a distinct algorithm to perform the task.
In some cases, you might want the `Strategy` to also have some attributes that are common to each `ConcreteStrategy`. In such cases, the `Strategy` can be an abstract class, with the `ConcreteStrategies` inheriting from it.
#### Advantages:
- The use of the Strategy pattern provides an alternative to class inheritance, allowing dynamic strategy changes.
- If an algorithm uses information that should not be exposed to clients, the Strategy pattern prevents these internal structures from being exposed.
- This design pattern is useful for switching between a large number of possible strategies.
#### Disadvantages:
- It increases the number of objects created, leading to a higher overhead in the exchange of objects between the strategy and the context.
### UML:
![](https://t12904266.p.clickup-attachments.com/t12904266/9c5e5e30-0587-4f58-9e55-7fab39841e15/image.png)
- **Context:** The element that uses the algorithms. It delegates to the strategy hierarchy. The context sets a specific strategy by referencing the necessary strategy and can, therefore, change the strategy as needed.
- **Strategy Interface:** Declares a common interface for all supported algorithms. This interface is used by the context to invoke the specific strategy. An abstract class may be used if common variables or methods are needed for different strategies.
- `ConcreteStrategy`: Implements the algorithm using the interface defined by the strategy. This class contains reusable logic that is isolated from the context.
### Functionality:
When the `Context` wants to use a specific algorithm, it first sets a variable (which will hold an object that implements the `Strategy` interface) with an appropriate value. Then, it invokes the method it wants to execute. The object that receives this invocation will be a `ConcreteStrategy`, which executes the method using its own algorithm.
## Example:
Let's assume we're designing an online store, and we want it to accept various payment methods (Credit Cards, PayPal, Bitcoin, etc.). A Strategy pattern architecture example for this scenario would look like the following. Here's the UML:
#### `Interface`:
```java
public interface StrategyPago {
  void pago();
}
```
#### Classes that implement `StrategyPago`:
##### Credit Card Payment class:
```java
public class Tarjeta implements StrategyPago {
  private String titular;
  private String numero;
  private String cvc;
  private String vencimiento;

  @Override
  public void pago() {
    System.out.println("Pagado con tarjeta");
  }
}
```
##### PayPal Payment class:
```java
public class Paypal implements StrategyPago {
  private String email;
  private String clave;

  @Override
  public void pago() {
    System.out.println("Pagado con PayPal");
  }
}
```
##### Bitcoin payment class:
```java
public class Paypal implements StrategyPago {
  private String email;
  private String clave;

  @Override
  public void pago() {
    System.out.println("Pagado con PayPal");
  }
}
```
#### Store class:
```java
public class Tienda {
  private StrategyPago formaPago;

  public void pago() {
    formaPago.pago();
  }

  public void setPago(StrategyPago nuevoPago) {
    formaPago = nuevoPago;
  }
}
```
### Explanation:
In this simplified example, we can use a `Tienda` object, set the payment method (from any of the classes that implement `StrategyPago`), and process the payment.
- **Interface `StrategyPago`:** Defines the `pago()` method that all payment strategies must implement.
- **Concrete Strategy Classes (`Tarjeta`, `Paypal`, `Bitcoin`):** Each of these classes implements the `pago()` method with the specific logic for processing a payment using that method.
- **`Tienda` Class:** This class uses a `StrategyPago` object to process payments. The `setPago()` method allows the store to switch between different payment methods dynamically.
#### Advantages:
The payment logic resides within each payment method rather than in the store itself, making the algorithm more modular and easier to manage. If a new payment method is needed, you only need to create a new class that implements `StrategyPago`.

This architecture clearly demonstrates how the Strategy pattern allows for flexibility and scalability in handling different payment methods.