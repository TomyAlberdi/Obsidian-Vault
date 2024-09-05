#Cheatsheet 
The `JOIN` command, as its name suggests, establishes joins between different tables that have some type of relationship with each other. Advantages of using JOIN:
- Much more understandable syntax
- Better performance.
- Provides certain flexibilities.
### Inner Join:
The INNER JOIN between two tables returns only the records that meet the condition specified in the ON clause.
```sql
SELECT column1, column2, ... 
FROM table_A 
INNER JOIN table_B ON condition
```
It is the default option and returns all records where two or more tables intersect. 
![[Pasted image 20240825161830.png]]
An example could be written as follows:
```sql
SELECT last_name, first_name, invoice.id, invoice.date 
FROM customer 
INNER JOIN invoice ON customer.id = invoice.customer_id;
```
### Left Join:
The LEFT JOIN between two tables returns all records from the first table, even when the records do not meet the condition specified in the ON clause.
```sql
SELECT column1, column2, ... 
FROM table_A 
LEFT JOIN table_B ON condition
```
It returns all records where two or more tables intersect, including the records from the first table that do not meet the condition specified in the ON clause. 
![[Pasted image 20240825161904.png]]
An example could be written as follows:
```sql
SELECT first_name, last_name, invoice.id, invoice.date 
FROM customer 
LEFT JOIN invoice ON customer.id = invoice.customer_id;
```
#### Left Excluding Join:
This type of LEFT JOIN returns only the records from the first table, excluding the records that meet the condition specified in the ON clause. 
![[Pasted image 20240825161939.png]]
An example could be written as follows:
```sql
SELECT first_name, last_name, invoice.id, invoice.date 
FROM customers 
LEFT JOIN invoice ON customer_id = invoice.customer_id 
WHERE invoice.id IS NULL;
```
### Right Join:
The RIGHT JOIN between two tables returns all records from the second table, even when the records do not meet the condition specified in the ON clause.
```sql
SELECT column1, column2, ... 
FROM table_A 
RIGHT JOIN table_B ON condition;
```
The RIGHT JOIN returns all records where two or more tables intersect, including the records from the second table that do not meet the condition specified in the ON clause. 
![[Pasted image 20240825162048.png]]
An example could be written as follows:
```sql
SELECT first_name, last_name, invoice.id, invoice.date 
FROM customer 
RIGHT JOIN invoice ON customer.id = invoice.customer_id;
```
#### Right Excluding Join:
This type of RIGHT JOIN returns only the records from the second table, excluding the records that meet the condition specified in the ON clause. 
![[Pasted image 20240825162130.png]]
An example could be written as follows:
```sql
SELECT first_name, last_name, invoice.id, invoice.date 
FROM customers 
RIGHT JOIN invoice ON customer.id = invoice.customer_id 
WHERE customer.id IS NULL;
```