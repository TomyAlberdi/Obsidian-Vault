Created: 2024-09-17 15:42
## Family Tree:
1. Computer
2. Backend Development
3. [[Java]]
-- -
### Equal Elements:
Collections such as `Set` (e.g., `HashSet`, `LinkedHashSet`, and `TreeSet`) do not accept duplicate or null values. The same applies to the keys in `Map`. But how do we determine if one object in a collection, such as a `Person`, is equal to another? We need to establish the criteria for equality, and if those criteria are not met, we consider the objects to be different.
In Java, to determine if two objects are equal, you must override the `equals()` and `hashCode()` methods. This allows collections to determine if the element they store is equal to another. For `Set` collections, this prevents duplicate insertion.
### Ordering Elements:
For collections like `TreeSet` and `TreeMap`, elements are stored in a sorted order. It's not enough to determine equality; we also need to compare elements to evaluate which is greater, lesser, or equal to another. In Java, this is achieved by implementing the `Comparable` interface.
We can use this interface to sort elements in a `List` (e.g., `ArrayList` or `LinkedList`) by invoking the `sort()` method.