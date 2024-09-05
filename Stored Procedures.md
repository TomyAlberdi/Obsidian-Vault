#Cheatsheet 
A stored procedure (SP) is a set of instructions in [[SQL]] format that are stored, compiled, and executed within the database server. They can include input and output parameters, return tabular or scalar results, send messages to the client, and invoke DDL and DML instructions. Generally, they are used to define business logic within the database and reduce the need to encode this logic in client programs.
### Structure
- `DELIMITER`: This clause is followed by a combination of symbols that will indicate the end of the SP.
- `CREATE PROCEDURE`: This command precedes the name we will give to the SP.
- `BEGIN`: Indicates the beginning of the SP code.
- `END`: Indicates the end of the SP code, followed by the combination of symbols defined in the delimiter.
```sql
DELIMITER $$
CREATE PROCEDURE sp_procedure_name()
BEGIN
  -- SQL instruction block
END $$
```
### Deleting an SP:
```sql
DROP PROCEDURE [IF EXISTS] sp_procedure_name
```
### Executing an SP:
```sql
CALL procedure_name(parameters);
```
### Advantages and Disadvantages
#### Advantages:
- **High response speed**: Everything is processed within the server.
- **Increased security**: Direct access to the tables where the data is stored is limited and prevented, avoiding direct manipulation by client applications.
- **Independence**: All code is within the database and does not depend on external files.
- **Code reuse**: Eliminates the need to rewrite a set of instructions.
- **Easier maintenance**: Reduces the cost of modification when business rules change.
#### Disadvantages:
- **Difficult modification**: If modification is required, its definition has to be completely replaced. In very complex databases, modification can affect other software pieces that directly or indirectly refer to it.
- **Increased memory usage**: If we use many stored procedures, the memory usage of each connection that uses those procedures will increase substantially.
- **Restricted for complex business logic**: In reality, stored procedure constructs are not designed to develop complex and flexible business logic.
### Variables
Within a stored procedure (SP), it is allowed to declare variables, which are elements that store data that can change throughout the execution. The declaration of variables is placed after the BEGIN clause and before the SQL instruction block. Optionally, an initial value can be defined using the DEFAULT command.
```sql
DECLARE variable_name DATA_TYPE [DEFAULT value];
```
To assign a value to a variable, the SET command is used. Variables can only contain scalar values, that is, a single value.
```sql
SET variable_name = expression;
```
Example:
```sql
DELIMITER $$ 
CREATE PROCEDURE sp_procedure_name() 
BEGIN 
  DECLARE salary FLOAT DEFAULT 1000; 
  SET salary = 2000; 
END $$
```
### Parameters
Parameters are variables through which data is sent and received from client programs. They are defined within the CREATE clause. Stored Procedures (SP) can have one, several, or no input or output parameters. There are three types of parameters:
- **IN**: Input parameter, receives data.
- **OUT**: Output parameter, returns data.
- **IN/OUT**: Input-output parameter, receives and returns data.
#### IN Declaration:
```sql
CREATE PROCEDURE procedure_name (IN param1 DATA_TYPE, IN param2 DATA_TYPE)
```
#### OUT Declaration:
```sql
CREATE PROCEDURE procedure_name (OUT param1 DATA_TYPE, OUT param2 DATA_TYPE)
```
The use of output parameters is done using the INTO command, as follows:
```sql
CREATE PROCEDURE sp_get_user_name (INOUT id INT, OUT user_name VARCHAR(30))
BEGIN
  SELECT name INTO user_name FROM user WHERE user_id = id;
END
```
#### IN/OUT Declaration:
Can receive values and return results in the same variable.
```sql
CREATE PROCEDURE procedure_name (INOUT param1 DATA_TYPE, INOUT param2 DATA_TYPE)
```