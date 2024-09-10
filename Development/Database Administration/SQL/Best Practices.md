The following recommendations aim to optimize query execution times and write solid [[SQL]] queries. When we do not implement these recommendations, SQL performs the analysis on all the tables being queried. If the table has numerous records, the time to return the result can harm the application.
### Create:
- We will try to use VARCHAR instead of TEXT: If you need to store very large text volumes, but they are less than 8000 characters, use the VARCHAR data type for its scalability.
- We will carefully evaluate the use of CHAR and VARCHAR: The use of CHAR and VARCHAR depends on whether the field in which it will be used varies greatly in size or not. This is to weigh speed performance over storage performance. The SQL engine processes fixed-length columns faster. Use CHAR for columns with little variation in length and VARCHAR for those that do not have a stable or average length.
- We will not use columns with FLOAT, REAL, or DATETIME data types as FOREIGN KEY.
- We will use CONSTRAINT to maintain data integrity.
- We will avoid COMPOSITE primary keys: Keep in mind that if we expect our table with a composite primary key to have millions of rows, the performance of CRUD operations will be very degraded. In that case, it is much better to use a simple ID primary key that has a compact enough index and establishes the necessary database engine constraints to maintain uniqueness.
### Select:
- We will avoid using `SELECT * FROM`: Although it is easy and convenient to use the wildcard to bring all fields, it should be omitted and instead specify the fields that need to be brought. The use of the wildcard also prevents effective and efficient use of indexes.
- Prefix the table ALIAS to each column: Specifying the table alias before each field defined in the SELECT saves the engine time from having to look up which table the specified field belongs to.
- We will avoid using GROUP BY, DISTINCT, and ORDER BY as much as possible: Avoid using these functions whenever possible, as they consume a large amount of resources. Consider that if it is really necessary to use them, the sorting of the results can be left to the application that will receive the data.
### Where:
- We will avoid using wildcards in LIKE such as `%value%`: In the case of using the LIKE statement, do not use the wildcard at the beginning of the string to search. This is because if applied, the search would have to read all the data in the table or tables involved to respond to the query. It is recommended that there are at least three characters before the wildcard.
- We will avoid using IN in subqueries, EXISTS is better: Promote the use of EXISTS and NOT EXISTS, instead of IN and NOT IN.
- We will try not to use functions within the WHERE conditions: SQL cannot efficiently search records when using functions, for example, conversion functions, within a column. In the conditions, try to use the original column format.
### Union:
- We will use UNION ALL to avoid an implicit distinct: In case of using the UNION statement and there is certainty that no duplicate records will be obtained in the involved SELECTs, then it is advisable in this scenario to replace UNION with UNION ALL to avoid the implicit use of the DISTINCT statement, as this increases resource usage.
### CRUD:
- We will use SET NOCOUNT ON with CRUD operations: Use SET NOCOUNT ON with CRUD operations to not count the number of affected rows and gain performance, especially in tables with many records.