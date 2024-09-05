#Theory 
Now that we have learned to model [[inheritance]] relationships and understand the concept of encapsulation, we will analyze how inheritance behaves in relation to encapsulation. Remember that when a property is **public**, it means it is accessible from any class. In other words, whenever an object wants to access a public value, it can obtain and modify it without any operation in between. This would be equivalent to not hiding information and, therefore, "breaking" encapsulation. 
On the contrary, if we declare an attribute as **private**, we completely limit access to the data. No one other than the class itself can access that data. Whenever you want to access or modify the data, you must perform an operation for that purpose, for example, through getters or setters. With inheritance, a new visibility modifier called **protected** appears, which in UML diagrams is specified with the “#”, allowing us to have intermediate visibility of the attribute or method declared as such. That is, it is private to other classes but public to child classes. The use of this visibility modifier "breaks" encapsulation, and we will avoid its use as much as possible as a best practice.
Example:

| Dog                                                    |
| ------------------------------------------------------ |
| - name: String (private)<br># age: Integer (protected) |
| + play() (public)                                      |
| # bark() (protected)                                   |
