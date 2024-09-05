#Theory 
An ORM is a programming model that allows mapping the structures of a [[database]] onto a logical structure of entities in our application. Therefore, we can say that it is a technique that allows the relationship between the objects of the source code of our application and the data they represent in the database.
**Why use ORM?** We must take into account that using ORMs introduces a code overhead in our applications to handle the data. For this reason, ORMs are especially recommended in:
- Applications with complex data models.
- Applications where performance is not critical.
ORMs are useful when managing transactions - INSERT/UPDATE/DELETE operations - but when it comes to collecting data with complex results, it is very important to evaluate the performance and efficiency of an ORM tool.
**Well-known ORMs:** Most ORMs are based on the same principles and often work very similarly. Each [[programming language]] can use its own ORM.
- Hibernate (Java)
- Entity Framework (.NET)
- Doctrine (PHP)
- SQLAlchemy (Python)
- ActiveRecord (Ruby)
### Advantages:
- No [[SQL]] code is used.
- Allows code reuse and improves code maintenance.
- Prevents SQL injection attacks.
- Performs data type conversion from the language to SQL.
### Disadvantages:
- Can delay projects due to the learning curve.
- Requires high code standardization and good application architecture.
- Can reduce performance.
- There is a possibility that it may be very complex.