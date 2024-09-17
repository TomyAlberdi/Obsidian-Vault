Created: 2024-09-17 16:59
## Family Tree:
1. Computer
2. [[Programming Theory]]
-- -
Many other languages use "parametric data types," sometimes referred to as genericity, where a generic data type is defined for a data structure or class that is specified at the time of use. In Java, this concept is known as Generics.
In short, Generics involves deferring the question "What type is this object?" Instead, the "type" of the object is left as a parameter that the programmer will specify when working with that object.
## Syntax and usage
In Java, to define a parametric data type, we use the symbols `<>`. Let’s look at a simple example: a bucket. It can contain many things: dirt, sand, water, fuel, etc. Here's how we can implement this in code:
```java
public class Bucket<T> {
  private T content;

  public Bucket() {}

  public void fill(T content) {
    this.content = content;
  }

  public T getContent() {
    return content;
  }
}
```
Here, when we define the `Bucket` class, we don't specify the type of its content; instead, we "defer" this decision until the moment of use. In other words, we leave the type as a parameter. This parameter is defined by the letter `T` (it can be any letter of the alphabet). `T` is commonly used to stand for Type. This also applies to operations on the content: we limit its use according to the type of the `content` attribute.
Now, assuming we have classes `Water`, `Sand`, `Fuel`, etc.:
```java
Water w = new Water();
Fuel f = new Fuel();
Bucket<Water> b = new Bucket<>();
b.fill(w);
b.fill(f); // This would not compile, as the bucket was defined with content of type "Water".
```
To solve this, we can use the `Object` type as the content type. This would allow the bucket to be filled with any other object.
```java
private Object content;
```
## Parametric Collections
To begin, remember that in all operations we perform on collections, the type used is `Object`.
- `add(Object o)`: `void`
- `get(int i)`: `Object`
- `iterator()`: `Iterator`
- `hasNext()`: `boolean`
- `next()`: `Object`
Since in Java all our classes inherit from `Object`, we can mix objects of different types in the same collection.
Example:
```java
List vehicles = new ArrayList();

Motorcycle moto = new Motorcycle();
Truck truck = new Truck();

// Add the vehicles to the list
vehicles.add(moto);
vehicles.add(truck);

// If at some point we want to retrieve a vehicle from the list, we must cast it.
Motorcycle moto = (Motorcycle) vehicles.get(0);
Truck truck = (Truck) vehicles.get(1);

// Iterate over the list
for (Object o : vehicles) {
  System.out.println(((Vehicle)o).isAvailable());
}

// If we want to load cargo onto the truck, we need to cast only those elements in the list that are trucks. Otherwise, we would have a runtime error.
for (Object o : vehicles) {
  if (o instanceof Truck) {
    ((Truck)o).load("sand");  
  }
}
```
Example with generics:
To avoid mixing different types of objects in a collection, all collections can be parameterized with a type, i.e., they support Generics.
```java
List<Truck> vehicles = new ArrayList<Truck>();
```
If we use collections with a specified type, we have compile-time control over the types of objects we add to the collection. This means that at runtime, there is no need to check with `instanceof` because casting is not required, as we cannot "mix" object types.
```java
for (Truck o : vehicles) {
  o.load("sand");
}
```