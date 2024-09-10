Different operations that are done regularly over [[Collections]].
### Creating a Collection
When creating a collection or any type of object, it is good practice to use the most generic reference type possible.
```java
List names = new ArrayList();
Set surnames = new HashSet();
Map ages = new TreeMap();
```
Since `ArrayList` and `LinkedList` implement the `List` interface, we will always treat these collections as `List`, as the operations we need to perform on these collections are defined by this interface. In contrast, `HashSet`, `LinkedHashSet`, and `TreeSet` implement the `Set` interface, so we will treat these collections as `Set`. Similarly, `HashMap`, `LinkedHashMap`, and `TreeMap` will be implemented as `Map`.
### Adding Elements:
Both the `List` and `Set` interfaces provide the `add` method, which takes an `Object` as a parameter, and since every class inherits from `Object`, we can store any type of object in them. On the other hand, the `Map` interface provides the `put` method.
```java
List names = new ArrayList();
names.add("Tomas");

Set surnames = new HashSet();
surnames.add("Alberdi");

Map ages = new TreeMap();
ages.put(30999888, 21);
```
### Removing Elements:
All collections have a `remove` method. For `List` implementations, you can remove by index or by value. For `Set` implementations, you can only remove elements by passing the value. For `Map` implementations, elements are removed by key.
```java
names.remove("Tomas");
names.remove(2);

surnames.remove("Alberdi");

ages.remove(23555888);
```
### Retrieving or Searching for Elements:
For `List`, if you want to get a value and know the index, you can use the `get` method, which takes the index as a parameter. For `Set`, you need to search by iterating through the collection, as `Set` does not have indices. For `Map`, to retrieve an element, you do so using its key.
```java
System.out.println(names.get(2));

boolean found = false;
String surname = null;
Iterator it = surnames.iterator();
while (it.hasNext() && !found) {
  surname = (String) it.next();
  if (surname.equals("Alberdi")) {
    found = true;
  }
}

ages.get(22888333);
```