## `For / While`
To iterate over a [[Collections|collection]] using a `for` or `while` loop, we need the `size()` and `get()` methods. Not all collections have these methods, so these options cannot be used with some collections. In other words, they can only be used with collections that extend the [[Collections#Interface `List`|List]] interface.
#### `For` loop:
```java
for (int i = 0; i < collection.size(); i++) {
  System.out.println(collection.get(i));
}
```
#### `While` loop:
```java
int i = 0;
boolean found = false;
while (i < collection.size() && !found) {
  if (collection.get(i).equals("Searched Element")) {
    found = true;
  }
  i++;
}
```
## `Iterator`
In Java, collections implement the Iterable interface, which requires implementing the `iterator()` method. This method returns an object of type Iterator, which allows you to traverse the collection using the `hasNext()` and `next()` methods.
```java
Iterator iterator = collection.iterator();
while (iterator.hasNext()) {
  System.out.println(iterator.next());
}
```
## `For Each`
Many languages provide a simple way to iterate over a collection using `for each` loops.
```java
for (Object obj : collection) {
  System.out.println(obj);
}
// For each object in the collection "collection", retrieve it and place it in the variable "obj".
```