Created: 2024-09-17 17:28
## Family Tree:
1. Computer
2. Programming Theory
3. Object-Oriented Programming
4. [[Design Patterns]]
-- -
Let’s learn how to reduce the complexity of interacting with a group of subsystems by providing a single entry point.
## Purpose
The **Facade** is a structural design pattern (Design Patterns > Structural Patterns) that provides a simplified interface to a library, framework, or any other complex group of classes.
## Solution
An interface is provided that defines how the client will communicate with the system. This class will implement the interface to receive requests and will be responsible for forwarding the client’s request to the appropriate class (subsystems).
## Advantages
- The software becomes more flexible and easier to expand.
- We reduce the use of objects that interact directly with the client, making the system easier to use.
- We reduce the coupling between the client and the subsystems, allowing us to modify the subsystems without affecting the client.
## Disadvantages
- High dependency on the facade interface.
## Implementation
Check if it’s possible to provide a simpler class than the one offered by an existing subsystem. We are on the right track if this interface makes the client code independent of many of the subsystem classes.
Declare and implement this interface in a new facade class. The facade should redirect calls from the client code to the appropriate objects in the subsystem. To fully leverage the pattern, ensure that all client code communicates with the subsystem solely through the facade. Now, the client code is protected from any changes in the subsystem code. For example, when a subsystem is updated to a new version, we will only need to modify the facade’s code.
If the facade becomes too large, consider extracting part of its behavior and placing it in a new refined facade class.
## Example
**Let’s suppose we need to design a system for an e-commerce platform.** Our client requests that when a product is purchased, our system should perform a series of steps, such as requesting the product from the warehouse, processing the payment, and sending the order.
Let’s see how we can solve this problem by applying this pattern.
### Implementation
Code for the interface `ICompraService`:
```java
public interface ICompraService {
    public void processPurchase(String productId, Integer quantity, Card card, Address address, List<Product> products);
}
```
Code for the class `CompraService`, our facade:
```java
public class CompraService implements ICompraService {

    private WarehouseService warehouseService;
    private PaymentService paymentService;
    private ShippingService shippingService;

    public CompraService() {
        this.warehouseService = new WarehouseService();
        this.paymentService = new PaymentService();
        this.shippingService = new ShippingService();
    }

    @Override
    public void processPurchase(String productId, Integer quantity, Card card, Address address, List<Product> products) {
        Product product;
        warehouseService.setProducts(products);
        product = warehouseService.findProduct(productId, quantity);
        if (product != null) {
            double amountToCharge = product.getValue() * quantity;
            if (paymentService.processPayment(card, amountToCharge)) {
                shippingService.processShipping(product, address);
            }
        }
    }
}
```
Code for the class `WarehouseService` (subsystem):
```java
public class WarehouseService {
    private List<Product> products;

    public void setProducts(List<Product> products) {
        this.products = products;
    }

    public Product findProduct(String productId, Integer quantity) {
        Product product = null;
        for (Product p : this.products) {
            if (p.getProductId().equals(productId) && p.getQuantity() >= quantity) {
                product = p;
                p.setQuantity(p.getQuantity() - quantity);
                product.setQuantity(quantity);
            }
        }
        return product;
    }
}
```
Code for the class `PaymentService` (subsystem):
```java
public class PaymentService {

    public Boolean processPayment(Card card, double amountToCharge) {
        Boolean paymentProcessed = Boolean.FALSE;
        if (card != null && card.getCardNumber() != null && card.getSecurityCode() != null) {
            System.out.println("Processing payment for " + amountToCharge);
            paymentProcessed = Boolean.TRUE;
        }
        return paymentProcessed;
    }
}
```
Code for the class `ShippingService` (subsystem):
```java
public class ShippingService {

    public void processShipping(Product product, Address address) {
        System.out.println("Shipping product to " + address.getStreet() + " " + address.getNumber() + ", " + address.getNeighborhood());
    }
}
```
Code for the `Main` class:
```java
import java.util.ArrayList;
import java.util.List;

public class Test {
    public static void main(String[] args) {
        List<Product> products = new ArrayList<>();
        Product productOne = new Product("1", 5, 1000, "Mouse");
        Product productTwo = new Product("2", 5, 3000, "Keyboard");
        products.add(productOne);
        products.add(productTwo);

        Card card = new Card("1111222233334444", "012", "2025/07/09");
        Address address = new Address("Av Monroe", "860", "1428", "CABA", "Capital Federal");

        ICompraService purchaseService = new CompraService();
        purchaseService.processPurchase("1", 2, card, address, products);
    }
}
```