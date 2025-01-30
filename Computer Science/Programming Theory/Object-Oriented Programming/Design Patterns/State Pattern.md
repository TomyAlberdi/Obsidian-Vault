Created: 2024-09-17 17:33
## Family Tree:
1. Computer
2. Programming Theory
3. Object-Oriented Programming
4. [[Computer Science/Programming Theory/Object-Oriented Programming/Design Patterns/Design Patterns]]
-- -
When an object is required to have different behaviors depending on its current state, it can become complex to manage the change in behaviors and states of that object. The **State** pattern (Design Patterns) offers a good solution to this complication by essentially creating an object for each possible state of the invoking object.
### Solution:
A class is implemented for each different state of the object, and each class will implement methods whose behavior varies according to that state. In this way, the object will always have a reference to a specific state and will communicate with it to fulfill its responsibilities.
### Advantages and disadvantages
##### Advantages:
- The responsibilities of specific states are easily localized because they are found in the classes corresponding to each state. This provides greater clarity in both development and subsequent maintenance.
- It makes state transitions explicit, as each state is represented in a class.
- Facilitates the expansion of states.
- Allows an object to change its class at runtime, as its responsibilities change from one object to another. Thus, the inheritance and responsibilities of the first object change to those of the second.
##### Disadvantages:
- It increases the number of subclasses.
### UML:
![[state_pattern_uml_diagram.jpg]]
- **Context Class:** Defines the interface with the client. The context instance defines its current state.
- **State Interface:** An interface for encapsulating the responsibilities associated with a particular state of the context. It defines the responsibilities of each state.
- **State Class:** Each state class implements the behavior or responsibility of the context. The context class sends messages to the state object within its code, which contains a state instance to assign the responsibility that the context object must fulfill. Thus, the context object changes its responsibilities according to the state it is in, as it also changes the state instance when a state change occurs.
### Summary:
The context tells the state instance to perform an action. However, when the state class instance changes (e.g., `StartState`, `StopState`, etc.), the action is performed differently according to the current state.
### Conclusion:
The pattern does not specify exactly where to define the transitions from one state to another. There are two ways to address this:
- **Defining these transitions within the context class.**
- **Defining these transitions in the State subclasses.**
The first solution is more convenient when the criteria are fixed, meaning they won't change. The second is preferable when the criteria are dynamic, which occurs when there is code dependency between the subclasses.
It's also important to evaluate in the implementation when to create different concrete state instances or use the same shared instance. This will depend on whether state changes are less frequent or more frequent, respectively.
## Example
We have a car that can have several states:
- `Off`: Without the ignition key and the engine stopped.
- `Stopped`: The engine is running but not moving.
- `Driving`: Moving on the road.
- `OutOfFuel`: Without fuel.
The car should have attributes to know its speed and the amount of fuel it has left.
The responsibilities might be:
- `Accelerate`: Increases speed and consumes fuel.
- `Ignition`: Used to start the car.
- `Brake`: Allows the car to stop.
State transitions occur when, for example:

| Situation                                  | New State |
| ------------------------------------------ | --------- |
| The car is off and I turn the ignition key | Stopped   |
| The car runs out of fuel                   | OutOfFuel |
| The car is stopped and I accelerate        | Driving   |
### Implementation:
```java
public class Car {
  // State of the car (off, stopped, driving, out of fuel)
  private StateCar state;
  private int currentSpeed = 0; // Current speed of the car
  private int currentFuel = 0;  // Remaining fuel

  public Car(int fuel) {
    this.setCurrentFuel(fuel);
    // Initial state (Off)
    this.setState(new Off(this));
  }

  public StateCar getState() { return this.state; }
  public void accelerate() { getState().accelerate(); }
  public void brake() { getState().brake(); }
  public void ignition() { getState().ignition(); }
  // Getters and setters are assumed
}

public interface StateCar {
  void accelerate();
  void brake();
  void ignition();
}

public class Off implements StateCar {
  // Reference to the context class
  private Car car;

  // Constructor that injects the dependency into the current class
  public Off(Car car) {
    this.car = car;
  }

  // Methods that do not work in this state (brake, accelerate) are assumed
  @Override
  public void ignition() {
    if (car.getCurrentFuel() > 0) {
      car.setState(new Stopped(car));
      car.setCurrentSpeed(0);
    } else {
      car.setState(new OutOfFuel(car));
    }
  }
}

public class Stopped implements StateCar {
  // Reference, constructor, and methods that do not work in this state (brake) are assumed

  @Override
  public void ignition() {
    car.setState(new Off(car));
  }

  @Override
  public void accelerate() {
    if (car.getCurrentFuel() > 0) {
      car.setState(new Driving(car));
      car.setCurrentSpeed(10);
      car.setCurrentFuel(car.getCurrentFuel() - 10);
    } else {
      car.setState(new OutOfFuel(car));
    }
  }
}

public class Driving implements StateCar {
  // Reference, constructor, and methods that do not work in this state (ignition) are assumed

  @Override
  public void accelerate() {
    if (car.getCurrentFuel() > 0) {
      if(car.getCurrentSpeed() >= 200) {
        car.setCurrentFuel(car.getCurrentFuel() - 10);
      } else {
        car.setCurrentSpeed(car.getCurrentSpeed() + 10);
        car.setCurrentFuel(car.getCurrentFuel() - 10);
      }
    } else {
      car.setState(new OutOfFuel(car));
    }
  }

  @Override
  public void brake() {
    car.setCurrentSpeed(car.getCurrentSpeed() - 10);
    if(car.getCurrentSpeed() <= 0) {
      car.setState(new Stopped(car));
    }
  }
}

public class OutOfFuel implements StateCar {
  // Reference, constructor, and methods that do not work in this state (ignition, brake, accelerate) are assumed
}
```
This implementation demonstrates how the car transitions between different states (Off, Stopped, Driving, OutOfFuel) depending on the actions performed and the current context. Each state has its own behavior, and the context (Car) changes its state and behavior accordingly.