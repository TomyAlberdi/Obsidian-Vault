#Language  #Cheatsheet #Development 
This [[Programming Language|language]] has a set of statements that we will gradually learn and add complexity to. SQL statements are grouped into two categories according to their functionality or purpose:
- **Data Definition Language (DDL)**: These are statements for creating tables and records. In other words, they are used to make modifications to the database structure.
- **Data Manipulation Language (DML)**: These are statements for querying, updating, and deleting data. In other words, they are used to perform queries and modifications on the records stored within each of the tables.
## Data Definition Statements
### Create Database:
With this command, we can create a database from scratch.
```sql
CREATE DATABASE nombre_database;
USE nombre_database;
```
### Create Table:
Allows you to create a table from scratch, along with its columns, types, and constraints.
```sql
CREATE TABLE peliculas (
  id INT PRIMARY KEY AUTO_INCREMENT,
  titulo VARCHAR(200) NOT NULL,
  premios INT DEFAULT 0,
  duracion INT NOT NULL,
  estreno DATE NOT NULL
)
```
##### Foreign Key:
When we create a table that has a foreign key, it will be necessary to use the FOREIGN KEY statement to clarify which table and column that data refers to. It is important to note that the "clients" table must exist before executing this statement to create the "orders" table.
```sql
CREATE TABLE orders (
  order_id INT NOT NULL,
  order_number INT NOT NULL,
  client_id INT,
  PRIMARY KEY (order_id),
  FOREIGN KEY (client_id) REFERENCES clients(id)
)
```
### Drop Table:
This command will delete the table specified in the statement.
```sql
DROP TABLE IF EXISTS movies;
```
### Alter Table:
Allows you to alter an existing table and operates with three commands.
- `Add` to add a column.
```sql
ALTER TABLE movies ADD rating DECIMAL(3,1) NOT NULL;
```
- `Modify` to modify a column.
```sql
ALTER TABLE movies MODIFY rating DECIMAL(4,1) NOT NULL;
```
- `Drop` to delete a column.
```sql
ALTER TABLE movies DROP rating;
```
## Data Manipulation Statements
### Insert:
There are two ways to add data to a table:
1. **Inserting data into all columns**: If we are inserting data into all columns, it is not necessary to specify the names of each column. However, the order in which we insert the values must be the same order as the columns assigned in the table.
```sql
INSERT INTO table_name (column1, column2, column3, ...) VALUES (value1, value2, value3, ...);
```
2. **Inserting data into specified columns**: To insert data into a specific column, we specify the table and then write the name of the column(s) in parentheses.
```sql
INSERT INTO table_name (specific_column) VALUES (specific_value);
```
### Update:
This command will modify the existing records of a table. As with DELETE, it is important not to forget the WHERE clause when writing the statement, specifying the condition. An example of a condition is `WHERE id = 4;` or `WHERE title = "name"`.
```sql
UPDATE table_name SET column1 = value1, column2 = value2, ... WHERE condition;
```
### Delete:
This allows us to delete information from a table. It is important to always use the WHERE clause in the statement to specify the condition of which rows we want to delete. If we do not write the WHERE clause, we would be deleting the entire table and not a particular record.
```sql
DELETE FROM table_name WHERE condition;
```
### Select:
Every query in the database will start with the word SELECT. Its functionality is to perform queries on one or more columns of a table. To specify which table we want to query, we use the word FROM followed by the name of the table.
```sql
SELECT column_name, column_name2, ... FROM table_name;
```
#### Where:
The functionality of WHERE is to condition and filter the SELECT queries that are made to a database.
```sql
SELECT column_name, column_name2, ...
FROM table_name
WHERE condition;
```
It uses traditional arithmetic operators in addition to:
- `IS NULL`: Is null.
- `BETWEEN`: Between two values.
- `IN`: List of values.
- `LIKE`: Matches.
#### Order By:
It is used to sort the results of a query according to the value of the specified column. By default, it is sorted in ascending order (ASC) according to the values of the column. It can also be sorted in descending order (DESC) by specifying it in the query.
```sql
SELECT column_name, column_name2, ...
FROM table_name
WHERE condition
ORDER BY column_name;
```
#### Between:
The **BETWEEN** operator is used when we need to obtain values within a range. **BETWEEN** includes the extremes. It works with numbers, texts, and dates. It is used as a filter in a **WHERE** clause. Example: With the following query, we would be selecting the name and age from the students table only when the ages are between 6 and 12.
```sql
SELECT name, age FROM students WHERE age BETWEEN 6 AND 12;
```
#### Like:
When we make a filter with a **WHERE** clause, we can specify a search pattern that allows us to specify something concrete that we want to find in the records. We achieve this by using wildcards. For example, we might want to search for:
- Names that have the letter "a" as the second character.
- Postal addresses that include the street "Monroe".
- Clients that start with "Los" and end with "s".
##### Wildcard `%`:
It is a substitute that represents zero, one, or several characters.
```sql
SELECT name FROM users WHERE address LIKE '%Monroe%';
```
Returns the addresses of users that include the word "Monroe".
##### Wildcard `_`:
It is a substitute for a single character.
```sql
SELECT name FROM users WHERE name LIKE '_a%';
```
Returns those names that have the letter "a" as the second character.
#### Limit:
Its functionality is to limit the number of rows (records/results) returned in SELECT queries. It also sets the maximum number of records to be deleted with DELETE.
```sql
SELECT column_name1, column_name2 FROM table_name LIMIT number_of_records;
```
#### Offset:
It allows us to specify from which row to start retrieving the requested data. For example, if we wanted to get all the data from a table but starting from position 10, the offset would have to be 9.
```sql
SELECT column_name1, column_name2 FROM table_name LIMIT number_of_records OFFSET number_of_skipped_records;
```
#### Alias:
Aliases are used to give a temporary and more friendly name to tables, columns, and functions. They are defined during a query and persist only during that query. To define an alias, we use the initials **AS** preceding the column we want to assign that alias to.
```sql
SELECT column_name1 AS alias_column_name1 FROM table_name;
```
##### Alias for a table:
```sql
SELECT name, surname, age FROM students_commission_start AS students;
```
In this way, we can give aliases to the columns and tables we are bringing in and make data manipulation more readable, always keeping in mind that aliases do not modify the original names in the database.
#### Aggregation functions:
MySQL comes with a large number of functionalities. Among them, aggregation functions are a tool we could consider as an ace up the sleeve. These will allow us to make the result of the queries show information, such as the number of records, the average, the total of certain information stored in a column, among others. The most common aggregation functions are:
- `COUNT`
- `AVG`
- `SUM`
- `MIN`
- `MAX`
As we can infer, the name itself gives a hint of the result we can obtain when implementing one of these functions.
##### COUNT:
Returns a single result indicating the number of rows/records that meet the criteria.
```sql
SELECT COUNT(*) FROM movies;
```
Returns the number of records in the movies table.
```sql
SELECT COUNT(id) AS total FROM movies WHERE genre_id=3;
```
Returns the number of records in the movies table with genre id 3 and shows it in a column named total.
##### AVG / SUM:
AVG or average returns a single result indicating the average of a column whose data type must be numeric.
```sql
SELECT AVG(rating) FROM movies;
```
Returns the average rating of the records in the movies table.
SUM returns a single result indicating the sum of a column whose data type must be numeric.
```sql
SELECT SUM(length) FROM movies;
```
Returns the sum of the durations of the records in the movies table.
##### MIN / MAX:
MIN returns a single result indicating the minimum value of a column whose data type must be numeric.
```sql
SELECT MIN(rating) FROM movies;
```
Returns the lowest rating of the record.
MAX returns a single result indicating the maximum value of a column whose data type must be numeric.
```sql
SELECT MAX(length) FROM movies;
```
Returns the longest duration in the movies table.
#### Group By:
The **GROUP BY** directive allows us to group the records of the resulting table from a query by one or more columns, as needed.
```sql
SELECT column_1
FROM table_name
WHERE condition
GROUP BY column_1;
```
**Example:** GROUP BY is used to group cars by brand, showing those with a manufacturing year equal to or greater than 2010.
```sql
SELECT brand
FROM cars
WHERE manufacturing_year >= 2010
GROUP BY brand;
```
Since GROUP BY groups the information, we lose the detail of each row. That is, we are no longer interested in the value of each row, but in the consolidated result among all rows.
**Conclusion:** The GROUP BY clause:
- Is used to group rows that contain the same values.
- Optionally, it is used together with aggregation functions to produce summary reports.
- Queries that contain the GROUP BY clause are called grouped queries and only return a single row for each grouped element.
#### Having:
The HAVING clause serves the same function as the WHERE clause, with the difference that HAVING allows the implementation of aliases and aggregation functions in the data selection conditions.
```sql
SELECT column_1
FROM table_name
WHERE condition
GROUP BY column_1
HAVING group_condition
ORDER BY column_1;
```
Example: The following query will return the number of customers per country (grouped by country). Only those countries with at least 3 customers will be included in the result.
```sql
SELECT country, COUNT(customerID)
FROM customers
GROUP BY country
HAVING COUNT(customerID) >= 3;
```
#### Table reference:
So far, we have seen queries (SELECT) within one table. But it is also possible and necessary to make queries to different tables and [[Join|join]] the results. For example, a possible scenario would be wanting to query a table where customer data is stored and another table where sales data to those customers is stored. Surely, in the sales table, there will be a field with the customer ID -`customer_ID`-.
```sql
SELECT customers.id, customers.name, sales.date 
-- Selects the columns id and name from the customers table, and the date column from the sales table
FROM customers, sales 
WHERE customers.id = sales.customer_id; 
-- Creates a condition to bring those records where the customer id is the same in both tables
```
#### Distinct:
When performing a query on a table, it may happen that the results contain two or more identical rows. In some situations, we may be asked for a list with non-duplicated records. For this, we use the DISTINCT clause which returns a list where each row must be distinct.
```sql
SELECT DISTINCT column_1, column_2 FROM table_name;
```
Complete example:
```sql
SELECT DISTINCT actor.first_name, actor.last_name 
FROM actor 
INNER JOIN actor_movie ON actor.id = actor_movie.actor_id 
INNER JOIN movie ON movie.id = actor_movie.movie_id 
WHERE movie.title LIKE "%Harry Potter%";
```
In this example, we see a query that asks for actors who have acted in any Harry Potter movie. If we did not write DISTINCT, actors who have participated in more than one movie would appear repeated in the result.