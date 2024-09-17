Created: 2024-09-17 15:57
## Family Tree:
1. Computer
2. Database Administration
3. [[SQL]]
-- -
An index within a database is a data structure that improves the speed of queries (SQL) by means of a unique identifier for each row in a table, allowing quick access to records in a database table. Let's look at an example of a student table: If we search for a student by their ID, it would be easy because this is a unique, ordered, and structured element. What happens if an application needs to search for students by email? Each time it needs to find a student, it will have to search cell by cell until it finds the requested email. With 3 rows, it's easy, but if we have a database of 1 million students and the query is performed repeatedly throughout the day, we will have performance problems, where each query will take time to respond. This is where indexes are used. An index is an additional structure where we choose one or more columns to be part of it. This will allow us to quickly locate the rows of the table based on their content in the indexed column(s).
**Advantages:**
- The use of indexes can improve query performance as the data needed to satisfy the query requirements exists in the index itself.
- They can significantly improve performance if the query contains aggregations (GROUP BY), table joins (JOINS), or a mix of both.
**Disadvantages:**
- The tables used to store indexes take up space.
- Indexes consume resources because each time an update, insertion, or deletion operation is performed on the indexed table, all the index tables defined on it must be updated - only the indexes defined on the updated columns need to be updated. For these reasons, it is not a good idea to define indexes indiscriminately.
**Considerations:**
- Avoid creating too many indexes on tables that are frequently updated and try to define them with the fewest possible columns.
- It is advisable to use a larger number of indexes to improve query performance on tables with few update needs but large volumes of data.
- It is recommended to use a short length in the key of clustered indexes. Clustered indexes also improve if they are created on unique columns or columns that do not allow NULL values.
### Types of indexes:
#### Simple:
Defined on a single column.
```sql
CREATE INDEX "I_books_author" ON "Books" (Author);
```
#### Composite:
Formed by several columns of the same table.
```sql
CREATE INDEX "I_books_authoreditor" ON "Books" (Author,Editor);
```
#### Unique:
Values must be unique and different. If we try to add a record with an existing value, an error message appears. It can also be simple or composite.
```sql
CREATE UNIQUE INDEX "I_books_author" ON "Books" (Author);
```
#### In other SQL engines:
##### Clustered index:
Stores row data in order. Only one clustered index can be created on a database table. This works efficiently only if the data is sorted in ascending or descending order.
```sql
CREATE CLUSTERED INDEX "I_books_author" ON "Books" (Author);
```
##### Non-clustered index:
Organizes data randomly, but the index internally specifies a logical order. The index order is not the same as the physical data order. Non-clustered indexes work well with tables where data is frequently modified, and the index is created on columns used in WHERE and JOIN statements.
```sql
CREATE NONCLUSTERED INDEX "I_books_author" ON "Books" (Author);
```
## Syntaxis:
- With `CREATE INDEX`, we can create an index by specifying the involved columns:
```sql
CREATE INDEX "Index_name" ON "Table_name" (Column_name);
```
- With `DROP INDEX`, we can delete an index from a specific table:
```sql
ALTER TABLE "Table_name" DROP INDEX "Index_name";
```
- With `ANALYZE TABLE`, we analyze and store the key distribution for a table:
```sql
ANALYZE TABLE "Table_name";
```