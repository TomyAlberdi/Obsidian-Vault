Let's imagine we have a system, a class with a few attributes, and we need to instantiate it a large number of times. The Flyweight [[Design Patterns|pattern]] allows us to have fewer instances and gives us the possibility to decorate them.
## Purpose
The pattern achieves this by sharing parts of an object's state among several objects. In other words, it abstracts the reusable parts, and instead of creating new objects every time they are required, we can reuse objects created by other instances. This helps reduce the memory capacity required by the application.
## Solution
This pattern has several components: the **client** is the object that triggers the execution. The `FlyweightFactory` is the factory we use to create flyweight or lightweight objects. The **flyweight** corresponds to the objects we want to reuse so they can be lighter.
## Advantages
- Significantly reduces the data load on the server.
## Disadvantages
- Takes a bit more time to perform searches.
## Example
Let's suppose we have a recipe book that contains recipes in different collections like meat, soups, salads, or in different categories such as Italian, Mexican, Argentinean, or fast food.
The recipe for a hamburger could be in several sections: fast food, meat, etc. If we needed to have a "hamburger recipe" object in each collection, it would be very inefficient and would use a lot of memory.
So, the client requests an object from the `FlyweightFactory`, which checks if it exists in the cache, and if not, creates a new one. **Flyweight** shares the state of the objects.
### Implementation
Code for the class that defines the method before creating the object. It checks if an identical object already exists. If it does, it returns the existing object. Otherwise, it creates the new object and stores it in the cache to be reused later.
```java
public class FoodFactory {
   private static final HashMap<String, Food> foodMap = new HashMap<>();

   public static Food getFood(String foodType) {
       Food food = (Food) foodMap.get(foodType);
       if (food == null) {
           food = new Food(foodType);
           foodMap.put(foodType, food);
           System.out.println("Creating food object of type: " + foodType);
       }
       return food;
   }
}
```
Food object with attributes for price, type, and whether it has lettuce:
```java
public class Food {
   private String foodType;
   private int price;
   private boolean hasLettuce;

   public Food(String foodType) {
       this.foodType = foodType;
   }

   public String getFoodType() {
       return foodType;
   }

   public int getPrice() {
       return price;
   }

   public void setPrice(int price) {
       this.price = price;
   }

   public boolean isHasLettuce() {
       return hasLettuce;
   }

   public void setHasLettuce(boolean hasLettuce) {
       this.hasLettuce = hasLettuce;
   }

   public void describeFood() { 
       System.out.println("It's a " + getFoodType() + " that costs: " + getPrice());
   }
}
```