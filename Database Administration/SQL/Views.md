Created: 2024-09-17 16:01
## Family Tree:
1. Computer
2. Database Administration
3. [[SQL]]
-- -
A view is a database element that facilitates access to table data. Basically, its function is to save a SELECT statement. This is a resource that allows us to visualize the results without worrying about how a query is defined. Views have the same structure as a table (rows and columns). The difference is that only the query definition is stored, not the data. In other words, a view is a virtual table based on the result set of an SQL query.
#### Utilities:
- Simplify data access when complex queries are required.
- Prevent data modification by third parties.
- Facilitate querying for those who do not know the data model or are not SQL experts.
#### Important Data:

- A view is executed at the moment it is invoked.
- View names must be unique (existing table names cannot be used).
- Only SELECT-type SQL statements can be included.
- View fields inherit the data types of the table.
- The result set returned by a view is unmodifiable, unlike the result set of a table.
### Creating Views:
A view is created with the CREATE VIEW clause.
```sql
CREATE VIEW view_name AS SQL query;
```
Example:
```sql
CREATE VIEW rock_songs AS 
SELECT songs.id, songs.name, genres.name AS genre 
FROM songs 
INNER JOIN genres ON songs.genre_id = genres.id 
WHERE genres.name IN ("Rock", "Rock and Roll");
```
### Modifying Views:
We use the ALTER VIEW clause to modify or replace a view.
```sql
ALTER VIEW view_name AS SQL query;
```
Example:
```sql
ALTER VIEW car_view AS  
SELECT * FROM car WHERE brand = "Fiat";
```
### Deleting Views:
We use the DROP VIEW clause to delete a view.
```sql
DROP VIEW view_name;
```
### Invoking Views:
Although views are different from tables, the invocation is the same as for a table. That is, the SELECT clause is used.
```sql
SELECT * FROM view_name;
```
Example:
```sql
SELECT * FROM car_view WHERE id > 10;
```