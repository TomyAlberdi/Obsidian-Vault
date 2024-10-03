Created: 2024-09-17 17:32
## Family Tree:
1. Computer
2. Programming Theory
3. Object-Oriented Programming
4. [[Programming Theory/Object-Oriented Programming/Design Patterns/Design Patterns]]
-- -
A certain object may have other objects that depend on it. These other objects might need to be updated when the state of the object they depend on changes. Implementing this logic can present many challenges. The observer pattern (Design Patterns) offers a solution by creating an interface that notifies and automatically updates all dependent objects whenever the state of the observed object changes.
There is an interface for the `ObservableSubject` (Observable) and one for the `Observers` (Observer). The concrete class that will be observed implements the `Observable` interface, while the concrete observers implement the `Observer` interface. These two interfaces have a method that must be declared by the concrete classes, and through these methods, the observers are updated whenever there is a state change in the `ObservableSubject`. This ensures that state updates are always received, regardless of the type of object, whether it be the observers or the observable subject.
#### Advantages:
- It allows subjects and observers to be modified independently. Objects can be reused without reusing their observers or vice versa. This adds scalability by allowing observers to be added without modifying the subject or other observers.
- Unlike a typical request, the notification sent by a subject does not need to specify its recipient. This creates a broadcast among all interested observers.
- Because the subject and observer are not tightly coupled, they can belong to different layers of abstraction within a system.
#### Disadvantages:
- An apparently harmless update to the subject can trigger a cascade of updates among the observers and their dependent objects. This can lead to false updates that are very difficult to track down.
### UML:
![](https://t12904266.p.clickup-attachments.com/t12904266/1a65f7de-dfe7-49f6-9bc2-9397fd5864fb/image.png)- **Observable Interface:** Each implementation is aware of its observers and can be observed by any number of observers. It also provides an interface for adding or removing observers.
- `Observer`: Defines an interface so that each implementation (`ConcreteObserver`) can update objects that need to be notified of changes in the subject.
- `ConcreteSubject`: Sends a notification to its observers when its state changes.
- `ConcreteObserver`: Maintains a reference to a `ConcreteSubject` object. It holds a state that should be consistent with that of the subject. It implements the observer’s update interface to keep its state synchronized with the subject’s state.
### Functionality:
When the `ObservableSubject` undergoes a state change, the `notify()` method is executed. This method iterates over a list containing all the objects observing the `ObservableSubject` and calls their `update()` method. This way, all observers remain updated with any changes without constantly needing to check for state updates.
### Conclusions:
- The pattern creates a direct dependency of each observer on the subject. While this can introduce complications, it is how the pattern is structured.
- The subject should not depend on any observer. This behavior would violate the subject’s ignorance of its observers and could create cyclic dependencies.
- It is advisable to specify the modifications of interest explicitly. Efficiency can be improved by extending the subject's registration interface to allow observers to register only for those specific events that interest them.
## Example:
Let's assume we have a system that displays the price of gold on a board, and when the price updates, it synchronizes with each subscribed instance, informing them of the price change.
![](https://t12904266.p.clickup-attachments.com/t12904266/fc8afb3d-ee4e-4fe5-8340-acab8c14f014/image.png)
#### `Interfaces`:
```java
public interface Observador {
  String actualizar();
}

public interface Observable {
  void agregar(Observador o);
  void quitar(Observador o);
  void notificar(String cambio);
}
```
#### Class `Pizarra`:
```java
import java.util.ArrayList;

public class Pizarra implements Observable {
  private float precioActual;
  private ArrayList<Observador> observadores = new ArrayList<>();
  
  public void cambiarPrecio(float precio) {
    this.precioActual = precio;
    notificar("Precio actualizado a: " + obtenerPrecio());
  }

  public float obtenerPrecio() {
    return this.precioActual;
  }

  @Override
  public void agregar(Observador o) {
    this.observadores.add(o);
  }

  @Override
  public void quitar(Observador o) {
    this.observadores.remove(o);
  }

  @Override
  public void notificar(String cambio) {
    for (Observador o: this.observadores) {
      System.out.println(o.actualizar() + cambio);
    }
  }
}
```
#### Class `Oro`:
```java
public class Oro implements Observador {
  @Override
  public String actualizar() {
    return this + "> Cambio de estado: ";
  }
}
```
#### `Main Class`:
```java
public class Main {
  public static void main(String[] args) {
    Pizarra pizarra = new Pizarra();
    Observador obs1 = new Oro();
    Observador obs2 = new Oro();
  
    pizarra.agregar(obs1);
    pizarra.agregar(obs2);

    pizarra.cambiarPrecio(42.5f);
    pizarra.cambiarPrecio(44.3f);
  }
}
```
### Explanation:
- **Interfaces:** `Observador` defines the `actualizar()` method that all observers must implement, while `Observable` defines methods to add, remove, and notify observers.
- **Class `Pizarra`:** Implements the `Observable` interface. It holds the current price of gold (`precioActual`) and a list of observers. When the price changes via `cambiarPrecio()`, it notifies all observers using the `notificar()` method.
- **Class `Oro`:** Implements the `Observador` interface. The `actualizar()` method returns a string indicating a state change.
- **Class `Main`:** The main class creates instances of `Pizarra` and `Oro`, adds observers to the `Pizarra`, and updates the price, triggering notifications to all observers.