Created: 2024-09-18 20:45
## Family Tree:
1. Computer
2. Database Administration
3. [[Data Analytics]]
-- -
A **data model** is an abstract model created with the goal of organizing data elements and standardizing relationships between business entities. In other words, data modeling defines the structure of data entities, their relationships, and their implementation based on the business nature.
In general, there are three main stages or types of models that make up data modeling:
1. **Conceptual Data Model**
2. **Logical Data Model**
3. **Physical Data Model**
## Conceptual Model
Describes what the data system should contain. Its goal is to identify business-relevant entities, their characteristics (attributes), and their relationships. For example: we have customers who place orders.
![[Database Administration/Data Analytics/attachments/image 1.png]]
A conceptual data model identifies the highest-level relationships between different entities.
- **Entities**: Objects or subjects in the database about which we want to store information. Examples include:
    - Customers
    - Salespeople
    - Branches
    - Products
- **Attributes**: These are the properties of each entity. Examples include:
    - First Name
    - Last Name
    - Branch_ID
    - Stock quantity
- **Relationships**: These establish links between pairs of entities. For example:
    - Each customer is served by a salesperson who works at a branch that holds products in stock.
## Logical Model
Describes how a data model should be implemented, regardless of the database management system (DBMS) used. It provides a more technical documentation of the conceptual model. For example: customers place orders, and each order should have only one associated customer. Orders include a date and a total amount.
![[Database Administration/Data Analytics/attachments/image 2.png]]
It is the more technical documentation of the conceptual model.
- **Entities**: All entities participating in the model are listed, and the primary key for each entity is identified.
- **Attributes**: All attributes for each entity are specified, and data normalization is performed.
- **Relationships**: All foreign keys (keys identifying relationships between different entities) are specified.
## Physical Model
Describes how the data model should be implemented within the specific database management system (DBMS). This includes defining tables, data types, primary keys, etc. 
![[Database Administration/Data Analytics/attachments/image 3.png]]For example: the orders table has an ID field, which is a primary key, integer, and non-nullable.
- **Entities**: Table names are defined.
- **Attributes**: Column names and definitions are provided along with data types and constraints.
- **Relationships**: All foreign keys (keys identifying relationships between entities) are specified.
## Conclusion

| Characteristic           | Conceptual | Logical | Physical |
| ------------------------ | ---------- | ------- | -------- |
| **Entity names**         | ✓          | ✓       |          |
| **Entity relationships** | ✓          | ✓       |          |
| Attributes               |            | ✓       |          |
| **Primary keys**         |            | ✓       | ✓        |
| **Foreign keys**         |            | ✓       | ✓        |
| **Table names**          |            |         | ✓        |
| **Column names**         |            |         | ✓        |
| **Column data types**    |            |         | ✓        |
