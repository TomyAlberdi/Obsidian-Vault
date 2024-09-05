#Development 
All classes we create in [[Java]] derive from the `Object` class, even if this is not explicitly stated. Because of this, when we create a new class, it inherits certain methods. We will focus on some of these methods, and to make them work correctly, we need to override them. The default behavior might cause errors or may not be the most appropriate.
### Methods to override:
- `String toString()`
- `boolean equals(Object o)`
- `int hashCode()`
#### `.toString()`:
Using this method will not result in an error, but the information displayed might not be understandable. The `toString()` method attempts to represent an object as text. The solution is to override the method to display only the information we want and format the output string appropriately. It's important not to change the method's signature, as doing so would result in overloading it.
Example:
```java
@Override
public String toString() {
  return "Name: " + name + "\n" + "Surname: " + surname;
}
```
#### `.equals(Object 0)`:
When we create an instance, what we have is a reference to the memory ([[Main Memory#RAM|RAM]]), meaning that data is not stored directly in the variable of the object type—only the reference to where the object's attribute values are located. This is why we cannot use the `==` operator to compare the equality between two objects because we would be comparing references.
To correctly compare objects, we must use the `equals()` method, which is inherited from the `Object` class. However, it doesn't always work correctly, so it's necessary to override it. This method takes an `Object` as a parameter, which presents an additional challenge.
Before working with `equals()`, we must consider what it means for two objects to be equal. For example, if we have a person, we might define them as equal if their surnames are the same. Therefore, when writing a class, one of the things we need to determine is how we will check for equality between two instances of that class.
##### **`instanceof` and `getClass`:** 
To start writing our `equals()`, we must consider that the parameter is an `Object`. We need to check if the object is an instance of the same class that we want to verify.
Two ways to check this:
1. `instanceof`:
```java
@Override
public boolean equals(Object o) {
  if (o == null) {
    return false;
  }
  if (!(o instanceof Person)) {
    return false;
  } else {
    // Rest of the comparison
  }
}   
```
2. `getClass()`:
```java
   @Override
public boolean equals(Object o) {
  if (o == null) {
    return false;
  }
  if (this.getClass() != o.getClass()) {
    return false;
  } else {
    // Rest of the comparison
  }
}
```
##### Casting:
Now we need to check for equality (in this case, having the same surname). We'll need to retrieve the surname from `o` to compare it with that of the instance. But since `o` is an `Object`, it doesn't "know" that it has a surname.
Therefore, we cast `o` and assign it to an object of type `Person`. By casting, we transform it so that we can assign it to an object of type `Person` and use its methods.
Next, we check if they have the same surname using the `equals()` method. Since `surname` is a `String` attribute, we cannot use the `==` operator.
Example:
```java
@Override
public boolean equals(Object o) {
  if (o == null) {
    return false;
  }
  if (!(o instanceof Person)) {
    return false;
  } else {
    Person auxPerson = (Person) o;
    return this.getSurname().equals(auxPerson.getSurname());
  }
}
```
#### `.hashCode()`:
When this method is used, it returns a unique number that identifies the object. For example, if I have two objects of the same class, `hashCode()` would generate a different number for each one, and that number would serve to identify it. The utility of this identifier will be discussed later. For now, we need to ensure that this identifier code is unique for each object.
Example:
```java
@Override
public int hashCode() {
  int hash = 31;
  hash = hash * name.hashCode();
  hash = hash * surname.hashCode();
  return hash;
}
```
To generate a unique number, we use prime numbers. Any prime number can be used; in this case, 31 is used. Since `name` and `surname` are strings, they are also objects and have their own `hashCode()`. We multiply all the numbers to obtain the object's `hashCode`. In a string, the `hashCode` is generated from the characters. The identifier will be different as long as the `name` and `surname` of the objects are different.