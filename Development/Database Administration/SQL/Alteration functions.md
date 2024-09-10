In many cases, we will need our [[SQL|query]] not only to bring the requested data but also to perform a couple of special operations with it. For example: unifying the data of two columns into one or perhaps setting a default value for all those records that are storing a null value. MySQL alteration functions will allow us to play a bit with the query result. Always keeping in mind that they will never alter the data originally stored in the database. The most common alteration functions are:
- `CONCAT`
- `COALESCE`
- `DATEDIFF`
- `TIMEDIFF`
- `EXTRACT`
- `REPLACE`
- `DATE_FORMAT`
- `DATE_ADD`
- `DATE_SUB`
- `CASE`
### CONCAT:
We use CONCAT to concatenate two or more expressions.
```sql
SELECT CONCAT('Name: ', last_name, ', ', first_name, '.') FROM actor;
```
### COALESCE:
We use COALESCE to substitute the NULL value in a sequence of expressions or fields. That is, if the first expression is NULL, it is replaced with the value of a second expression.
```sql
SELECT COALESCE(NULL, 'No Data');
```
### DATEDIFF:
We use DATEDIFF to return the difference between two dates, taking the specified interval as granularity.
```sql
SELECT DATEDIFF('2021-01-15', '2021-01-05');
```
### TIMEDIFF:
We use TIMEDIFF to return the difference between two times, taking the specified interval as granularity.
```sql
SELECT TIMEDIFF('18:45:00', '12:30:00');
```
### EXTRACT:
We use EXTRACT to extract parts of a date.
```sql
SELECT EXTRACT(HOUR FROM '2014-02-13 08:44:21'); -- '08'
```
### REPLACE:
We use REPLACE to replace a string of characters with another value. It should be noted that this function distinguishes between uppercase and lowercase.
```sql
SELECT REPLACE('Good afternoon', 'afternoon', 'evening'); -- 'Good evening'
```
### DATE_FORMAT:
We use DATE_FORMAT to change the output format of a date according to a given condition.
```sql
SELECT DATE_FORMAT('2017-06-15', '%W %M %e %Y'); -- Thursday June 15 2017
```
### DATE_ADD:
We use DATE_ADD to add a period of time to a DATE or DATETIME value.
```sql
SELECT DATE_ADD('2021-06-30', INTERVAL '3' DAY); -- 2021-07-03
```
### DATE_SUB:
We use DATE_SUB to subtract a period of time from a DATE or DATETIME value.
```sql
SELECT DATE_SUB('2021-06-30', INTERVAL '9' MONTH); -- 2020-09-30
```
### CASE:
We use CASE to evaluate conditions and return the first condition that is met. In this example, the resulting table will have 4 columns: id, title, rating, and rating_description. This last column will show the values: Bad, Regular, Good, and Excellent according to the movie's rating.
```sql
SELECT id, title, rating, CASE WHEN rating < 4 THEN 'Bad' WHEN rating BETWEEN 4 AND 6 THEN 'Regular' WHEN rating BETWEEN 7 AND 9 THEN 'Good' ELSE 'Excellent' END AS rating_description FROM movies;
```