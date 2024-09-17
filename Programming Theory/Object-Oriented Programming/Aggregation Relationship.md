Created: 2024-09-17 17:07
## Family Tree:
1. Computer
2. Programming Theory
3. [[Object-Oriented Programming]]
-- -
A very common case of relationships between classes is called aggregation, where there is a relationship between the aggregates and the whole, but the components can exist even if the whole is destroyed. In other words, it is a relationship that indicates that one class is part of another class or classes with a weak relationship, such that there is independence regarding their existence. We also say that aggregation is a "part of" relationship.

Example: A bicycle is made up of various elements (objects), such as wheels, pedals, brakes, and frame. Through an assembly process, we join the elements and form a bicycle. What happens if we perform the reverse process? If we disassemble the bicycle, do the other elements still exist and fulfill their purpose? The answer is yes, as each element can be used in another bicycle or even in another type of transport. This is where the issue lies; the objects have a weak relationship with the bicycle and can continue to exist even after we disassemble the bicycle.