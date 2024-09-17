Created: 2024-09-17 15:40
## Family Tree:
1. Computer
2. Backend Development
3. [[Java]]
-- -
Different ways to store data in Java.
## Interface `List`
#### `ArrayList`:
Stores elements contiguously, providing sequential access to them. It is very efficient when storing and accessing elements directly by their position (index). Its most important methods are:
- `.add(Object o)`: Adds an element.
- `.add(Object o, int pos)`: Adds an element at a specified position.
- `.remove(Object o)`: Removes an element.
- `.remove(int pos)`: Removes an element at a specified position.
- `.get(int pos)`: Gets the element at a specified position.
- `.size()`: Returns the number of elements in the list. Due to its characteristics, this will be the collection we use the most.
#### `LinkedList`:
This implementation performs better when making insertions near the middle of the list, i.e., when manipulating its elements. It is less efficient when only adding or accessing elements, where `ArrayList` is a better option. Its methods are the same as those of `ArrayList`.
## Interface `Set`
#### `HashSet`:
Unlike `ArrayList` and `LinkedList`, `HashSet` cannot store duplicate or null values. It is the highest-performing implementation, but it does not guarantee any order when traversing it. This means elements are not in the order they were inserted, and it does not have a `get` method. Its most important methods are:
- `.add(Object o)`
- `.remove(Object o)`
- `.size()`
#### `LinkedHashSet`:
Cannot store duplicated or null values, but elements are stored in the order of insertion. Thus, when traversing it, elements will be in the same order they were inserted. It is slightly less performant than `HashSet` and doesn't have a `get` method. Its most important methods are the same as those of `HashSet`.
#### `TreeSet`:
Implements the `Set` interface but also inherits from a class called `SortedSet`, which allows `TreeSet` to store elements according to their values. Its most important methods are the same as those of `HashSet` and `LinkedHashSet`.
## Interface `Map`
#### `HashMap`:
Maps are collections of key-value pairs. It is reasonable to assume that keys cannot be repeated, and each key corresponds to only one value. In both `HashMap` and `HashSet`, elements are not stored in the order of insertion. Its most important methods are:
- `.put(Object key, Object value)`: Adds an element.
- `.get(Object key)`: Retrieves an element based on a specified key.
- `.remove(Object key)`: Removes an element based on a specified key.
- `.size()`
#### `LinkedHashMap`:
Unlike `HashMap`, elements are stored according to the order of insertion. Its most important methods are the same as those of `HashMap`.
#### `TreeMap`:
Elements are stored in an ordered manner according to their keys. It is important to note that they are ordered by key, not by the value of the object they store. Its most important methods are the same as those of `HashMap` and `LinkedHashMap`.