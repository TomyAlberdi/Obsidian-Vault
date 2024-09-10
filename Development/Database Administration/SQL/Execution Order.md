The server does not read the query exactly in the order we write it. Once we click execute, the server receives the [[SQL|query]] and rearranges it to interpret each part of our code and respond as quickly as possible. How is a query processed? Complete execution order:
1. `FROM`
2. `JOIN`
3. `ON`
4. `WHERE`
5. `GROUP BY`
6. `HAVING`
7. `SELECT`
8. `DISTINCT`
9. `ORDER BY`
10. `LIMIT`
### Step 1: `FROM`, `JOIN`, `ON`
The table(s) from which we need the information are obtained. This is why it is the first block to be executed. We need to be clear about where to get the data and their join conditions.
### Step 2: `WHERE`
This is where we apply the necessary filters. One common error is trying to use the alias of a column that is in the SELECT. This generates an error because that column has not yet been created.
### Step 3: `GROUP BY`
Once the rows we need are filtered, we can use the GROUP BY statement to group results. Remember that columns not using an aggregate statement must be listed in this phase. As in the previous step, we should not use aliases.
### Step 4: `HAVING`
This is similar to step 4, but here we filter the results of step 5, which is why it is executed at this stage.
### Step 5: `SELECT`
In this phase, columns are created from the functions we have indicated, such as YEAR, COUNT, AVG, among others. We can also use statements like CASE WHEN, IF.
### Step 6: `DISTINCT`
Once the result is calculated, if we need to remove duplicates, it is done at this stage. This step is optional.
### Step 7: `ORDER BY`
This is the last phase and the only one where we can use the aliases declared in the SELECT phase since it is executed previously.
### Step 8: `LIMIT`
The final step is responsible for limiting the number of results to be displayed. It is a presentation option, not a calculation.