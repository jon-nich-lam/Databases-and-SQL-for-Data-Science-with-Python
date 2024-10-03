The order of evaluation in SQL queries, when all clauses are present, generally follows this sequence:

1. **FROM**: SQL first identifies the tables or data sources and gathers the raw data.
2. **WHERE**: Filters individual rows based on specified conditions.
3. **GROUP BY**: Groups the filtered rows based on the columns specified in the `GROUP BY` clause.
4. **HAVING**: Filters the groups formed in the previous step based on conditions applied to aggregate functions or group-based criteria.
5. **SELECT**: SQL retrieves the specified columns or expressions from the remaining rows or groups.
6. **ORDER BY**: Finally, SQL sorts the result set based on the specified columns.

### Step-by-Step Execution Order

1. **FROM**: 
   - The data source (e.g., table) is determined. If any joins or subqueries are involved, they are processed first.
   
   ```sql
   SELECT * FROM employees;
   ```

2. **WHERE**:
   - The `WHERE` clause filters rows based on conditions applied to the raw data.
   
   ```sql
   SELECT * FROM employees
   WHERE salary > 40000;
   ```

3. **GROUP BY**:
   - The `GROUP BY` clause groups the filtered rows based on one or more columns.
   
   ```sql
   SELECT department_id, COUNT(*)
   FROM employees
   WHERE salary > 40000
   GROUP BY department_id;
   ```

4. **HAVING**:
   - The `HAVING` clause filters the groups that were formed by `GROUP BY`. It allows you to apply conditions on aggregated data, such as `COUNT()`, `SUM()`, etc.
   
   ```sql
   SELECT department_id, COUNT(*)
   FROM employees
   WHERE salary > 40000
   GROUP BY department_id
   HAVING COUNT(*) > 5;
   ```

5. **SELECT**:
   - The `SELECT` clause specifies which columns or expressions to retrieve from the remaining rows or groups. It is evaluated after all previous steps are done.
   
   ```sql
   SELECT department_id, COUNT(*)
   FROM employees
   WHERE salary > 40000
   GROUP BY department_id
   HAVING COUNT(*) > 5;
   ```

6. **ORDER BY**:
   - Finally, the `ORDER BY` clause sorts the result set based on the columns specified.
   
   ```sql
   SELECT department_id, COUNT(*) AS num_employees
   FROM employees
   WHERE salary > 40000
   GROUP BY department_id
   HAVING COUNT(*) > 5
   ORDER BY num_employees DESC;
   ```

### Example in Full Context

Suppose you want to find departments where more than 5 employees earn a salary over $40,000, and you want to list these departments in descending order of the number of employees.

The query would look like this:

```sql
SELECT department_id, COUNT(*) AS num_employees
FROM employees
WHERE salary > 40000
GROUP BY department_id
HAVING COUNT(*) > 5
ORDER BY num_employees DESC;
```

### Summary of SQL Query Execution Order:

1. **FROM**: Get the data.
2. **WHERE**: Filter the data.
3. **GROUP BY**: Group the filtered data.
4. **HAVING**: Filter the groups.
5. **SELECT**: Retrieve columns.
6. **ORDER BY**: Sort the result set.

Understanding this execution order is crucial when writing complex SQL queries, especially when using aggregates, filtering, and sorting together.