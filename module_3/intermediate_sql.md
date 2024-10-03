
# Retrieving Data with SELECT Statement String Patterns

## Introduction
- The **main purpose** of a Database Management System (DBMS) is to **store** and **retrieve** data efficiently.
- The **SELECT statement** is used to **retrieve** data from a database.

### Simple SELECT Statements:
- In its simplest form, a **SELECT statement** is:
  
  ```sql
  SELECT * FROM table_name;
  ```

- Example with a table `Book`:
  
  ```sql
  SELECT * FROM Book;
  ```
  - Retrieves all rows and all columns.

- To retrieve specific columns:
  
  ```sql
  SELECT Book_ID, Title FROM Book;
  ```

- To **restrict** the result set using the **WHERE clause**:
  
  ```sql
  SELECT Title FROM Book WHERE Book_ID = 'B1';
  ```

## Using String Patterns
- **WHERE clause** requires a **predicate** (a condition that evaluates to true, false, or unknown).
- **What if we don't know the exact value?**
  - Example: We remember the author's first name starts with **R**.

- Use the **LIKE** predicate with **wildcards**:
  - The **percent sign (%)** is a wildcard that substitutes for any number of characters.

  ```sql
  SELECT first_name FROM author WHERE first_name LIKE 'R%';
  ```
  - This retrieves all authors whose first name starts with **R** (e.g., Raul, Rav).

## Using Ranges with `BETWEEN` and `AND`
- Instead of using **comparison operators** (greater than, less than), you can use the **BETWEEN** operator for **ranges**.

- Example: Retrieve books with pages between **290 and 300**:

  ```sql
  SELECT * FROM Book WHERE pages BETWEEN 290 AND 300;
  ```
  - This is **inclusive** of the range specified.

## Using Sets with `IN`
- The **IN** operator simplifies cases where multiple values need to be matched.
- Example: Retrieve authors from **Australia**, **Brazil**, or **Canada**:

  ```sql
  SELECT * FROM author WHERE country IN ('Australia', 'Brazil', 'Canada');
  ```
  - This simplifies the query, avoiding repeated conditions for each value.

## Summary
- The SELECT statement can be simplified using:
  1. **String patterns** with the `LIKE` operator.
  2. **Ranges** with the `BETWEEN AND` operator.
  3. **Sets** with the `IN` operator.


# Sorting SELECT Statement Result Sets

## Introduction
- The main purpose of a Database Management System (DBMS) is to **store** and **retrieve** data efficiently.
- In this lesson, we'll focus on sorting data retrieved from a database table using the **ORDER BY** clause.

### Simple SELECT Statement:
- In its simplest form, a **SELECT statement** is:

  ```sql
  SELECT * FROM table_name;
  ```

- Example with a table `Book`:
  
  ```sql
  SELECT * FROM Book;
  ```
  - Retrieves all rows and columns, but no particular order is applied.

- To retrieve only specific columns:
  
  ```sql
  SELECT title FROM Book;
  ```

  - This lists all book titles but **not in any specific order**.

## Using the ORDER BY Clause
- **ORDER BY** allows you to sort the result set by a specified column.
- By default, the sorting order is **ascending**.

- Example: Sorting by book title in **ascending alphabetical order**:

  ```sql
  SELECT title FROM Book ORDER BY title;
  ```

  - The result set is now sorted alphabetically by the `title` column.

### Sorting in Descending Order
- To sort the result set in **descending order**, use the `DESC` keyword.

- Example: Sorting book titles in **descending alphabetical order**:

  ```sql
  SELECT title FROM Book ORDER BY title DESC;
  ```

  - The result set is sorted with titles from **Z to A**.

### Sorting by Multiple Columns
- If the first few characters are the same, sorting will proceed based on the **next characters** in the column.

### Sorting by Column Sequence Number
- You can specify the **column sequence number** instead of the column name in the `ORDER BY` clause.

- Example: Sorting by the **second column** (number of pages):

  ```sql
  SELECT title, pages FROM Book ORDER BY 2;
  ```

  - The result set is sorted by the second column (`pages`), in **ascending order** by default.

## Summary
- **ORDER BY** allows sorting result sets in **ascending** or **descending** order.
- You can sort by:
  1. Column name.
  2. Column sequence number.


# Grouping SELECT Statement Result Sets

## Introduction
- In this lesson, we will focus on **grouping** and **eliminating duplicates** from SELECT statement result sets.
- We will learn how to use the **DISTINCT** keyword, the **GROUP BY** clause, and the **HAVING** clause to further refine result sets.

### Eliminating Duplicates with `DISTINCT`
- **Duplicate values** can appear in a result set if multiple rows share the same data.
- To remove duplicates, use the **DISTINCT** keyword.

- Example: Selecting distinct countries from the `author` table:

  ```sql
  SELECT DISTINCT country FROM author ORDER BY 1;
  ```

  - This will return a list of unique countries, eliminating duplicates.

### Grouping Results with `GROUP BY`
- The **GROUP BY** clause groups rows that have the same values in specified columns.
- It is often used with **aggregate functions** (e.g., `COUNT`, `SUM`, `AVG`) to perform calculations on groups of data.

- Example: Counting the number of authors from each country:

  ```sql
  SELECT country, COUNT(country) FROM author GROUP BY country;
  ```

  - This groups authors by country and returns the count of authors for each country.

### Using `AS` to Rename Columns
- When performing calculations, the resulting columns may not have clear names.
- Use the **AS** keyword to give a meaningful name to the calculated columns.

- Example: Renaming the `COUNT(country)` result to "Count":

  ```sql
  SELECT country, COUNT(country) AS Count FROM author GROUP BY country;
  ```

  - The result set now displays the `Count` of authors from each country.

### Restricting Results with `HAVING`
- The **HAVING** clause is used to filter groups based on conditions, similar to the **WHERE** clause but specifically for groups created by `GROUP BY`.
- **WHERE** filters rows, while **HAVING** filters groups.

- Example: Only display countries with more than 4 authors:

  ```sql
  SELECT country, COUNT(country) AS Count
  FROM author
  GROUP BY country
  HAVING COUNT(*) > 4;
  ```

  - This restricts the result set to countries with 5 or more authors (e.g., China and India).

# Functions, Multiple Tables, and Sub-Queries

## Summary
- **DISTINCT** removes duplicate values from a result set.
- **GROUP BY** groups rows that have the same values in specified columns.
- **HAVING** filters groups based on conditions, often using aggregate functions like `COUNT`.
- You can use **AS** to rename calculated columns for clarity.

### SQL Built-in Functions
- **Built-in functions** in SQL help reduce network traffic and bandwidth usage by performing operations within the database, making it faster, especially when working with large data sets.
- Functions can be included in SQL statements, such as `SELECT`, to manipulate and calculate data.

### Aggregate Functions
- **Aggregate functions** take a collection of values (usually from a column) and return a single value. These include:
  - **SUM**: Adds all values in a column. 
    Example: `SELECT SUM(COST) FROM PETRESCUE;`
  - **MIN**: Finds the lowest value in a column.
    Example: `SELECT MIN(ID) FROM PETRESCUE WHERE ANIMAL = 'Dog';`
  - **MAX**: Finds the highest value in a column.
    Example: `SELECT MAX(QUANTITY) FROM PETRESCUE;`
  - **AVG**: Calculates the average value in a column.
    Example: `SELECT AVG(COST) FROM PETRESCUE;`

- You can name the result of an aggregate function using `AS`.  
  Example: `SELECT SUM(COST) AS SUM_OF_COST FROM PETRESCUE;`

### Mathematical Operations with Aggregate Functions
- You can perform mathematical operations between columns before applying aggregate functions. 
  Example: To calculate the average cost per dog rescue, you could divide the cost by the quantity before averaging:
  ```sql
  SELECT AVG(COST / QUANTITY) FROM PETRESCUE WHERE ANIMAL = 'Dog';
  ```

### Scalar Functions
- **Scalar functions** operate on individual values and return a single value for each row in the result set. Some common scalar functions include:
  - **ROUND**: Rounds a number to the nearest integer.
    Example: `SELECT ROUND(COST) FROM PETRESCUE;`
  
### String Functions
- **String functions** are used to perform operations on text data (`char`, `varchar`). Examples include:
  - **LENGTH**: Returns the length of a string.
    Example: `SELECT LENGTH(ANIMAL) FROM PETRESCUE;`
  - **UPPER**: Converts a string to uppercase.
    Example: `SELECT UPPER(ANIMAL) FROM PETRESCUE;`
  - **LOWER**: Converts a string to lowercase.
    Example: `SELECT LOWER(ANIMAL) FROM PETRESCUE WHERE ANIMAL = 'Cat';`
  
  String functions can also be used in the `WHERE` clause for case-insensitive matching.

### Combining Functions
- Functions can be combined. For example, you can retrieve distinct values in uppercase by combining the `DISTINCT` and `UPPER` functions:
  ```sql
  SELECT DISTINCT(UPPER(ANIMAL)) FROM PETRESCUE;
  ```

### Conclusion
In summary, SQL provides various built-in functions, including aggregate functions for summarizing data and scalar/string functions for manipulating individual values. Using these functions effectively can help you retrieve and manipulate data directly in the database without needing to first extract it into your application.


### SQL Date and Time Types
- **SQL** provides special data types for handling dates and times:
  - **Date**: Contains 8 digits in the format `YYYYMMDD` (Year, Month, Day).
  - **Time**: Contains 6 digits in the format `HHMMSS` (Hour, Minute, Second).
  - **Timestamp**: Contains 20 digits in the format `YYYYMMDDHHMMSSZZZZZZ` (Year, Month, Day, Hour, Minute, Second, Microseconds).
  
### Extracting Date and Time Components
- SQL provides functions to extract specific parts of date and time, such as:
  - **Day**: Extracts the day portion of a date.
  - **Month**: Extracts the month.
  - **Hour, Minute, Second**: Extracts the respective time components.
  
  Example: To extract the day from a rescue date where the animal is a cat:
  ```sql
  SELECT DAY(rescue_date) FROM pet_rescue WHERE animal = 'Cat';
  ```

### Using Date and Time Functions in WHERE Clause
- Date and time functions can be used in the `WHERE` clause to filter results based on specific date or time components.
  
  Example: To count the number of rescues in May (Month = 5):
  ```sql
  SELECT COUNT(*) FROM pet_rescue WHERE MONTH(rescue_date) = 5;
  ```

### Date and Time Arithmetic
- SQL allows you to perform arithmetic with dates and times. For example, you can add or subtract days, months, or years from a date.
  - **DATE_ADD**: Adds a specified interval (e.g., days, months, years) to a date.
  
  Example: To find the date three days after each rescue date:
  ```sql
  SELECT DATE_ADD(rescue_date, INTERVAL 3 DAY) FROM pet_rescue;
  ```

### Special Registers for Current Date and Time
- **SQL** provides special registers like `CURRENT_DATE` and `CURRENT_TIME` to get the current system date and time.
  
  Example: To find how many days have passed since each rescue date:
  ```sql
  SELECT CURRENT_DATE - rescue_date FROM pet_rescue;
  ```

### Summary
- SQL contains **date**, **time**, and **timestamp** types for managing date and time data.
- Functions exist to extract components like day, month, hour, and more.
- Date and time functions can be used in the `WHERE` clause for filtering.
- You can perform **date arithmetic** using functions like `DATE_ADD` to calculate future or past dates.
- Special registers like `CURRENT_DATE` provide real-time system values.

This lesson provides a foundation for working with dates and times in SQL, allowing for precise data manipulation involving temporal data.

In this lesson, we covered **subqueries** (also known as **nested queries**) in SQL and how they can be used to write more powerful queries. Here's a summary of the key concepts discussed:

### What is a Subquery?
- A **subquery** is a query nested inside another query, typically enclosed in parentheses.
- Subqueries can be used to perform operations that would not be possible in a single query.
  
### Example Scenario: Retrieving Employees with a Salary Above the Average
- Suppose we want to retrieve the list of employees who earn more than the average salary.
- We cannot directly evaluate aggregate functions like `AVG()` in the `WHERE` clause.
  
  Example (incorrect query):
  ```sql
  SELECT * FROM employees WHERE salary > AVG(salary);
  ```
  - This results in an error because aggregate functions cannot be directly evaluated in the `WHERE` clause.
  
  Correct approach using a subquery:
  ```sql
  SELECT employee_ID, first_name, last_name, salary
  FROM employees
  WHERE salary > (SELECT AVG(salary) FROM employees);
  ```
  - The subquery calculates the average salary, which is then compared with the salary in the outer query.

### Subqueries in Different Clauses
- **Subqueries in the `WHERE` clause**: As shown in the example above, subqueries are commonly used in the `WHERE` clause to compare values against the result of the subquery.

- **Subqueries as Column Expressions**: Subqueries can also be placed in the list of columns to be selected.
  
  Example: Comparing each employee’s salary with the average salary:
  ```sql
  SELECT employee_ID, salary, 
         (SELECT AVG(salary) FROM employees) AS average_salary
  FROM employees;
  ```
  - This query retrieves the salary of each employee along with the average salary.

### Derived Tables or Table Expressions
- A **derived table** (or **table expression**) is a subquery used in the `FROM` clause. It acts as a temporary table that can be used as a data source in the outer query.
  
  Example: Creating a derived table with non-sensitive employee information:
  ```sql
  SELECT * FROM 
  (SELECT employee_ID, first_name, last_name, department_ID 
   FROM employees) AS employee_info;
  ```
  - The subquery creates a temporary table `employee_info`, which excludes sensitive information like date of birth or salary.

### Benefits of Subqueries
- **Overcoming limitations**: Subqueries help bypass certain SQL limitations, such as the inability to use aggregate functions directly in the `WHERE` clause.
- **Richer queries**: Subqueries allow for more complex queries by providing intermediate results that can be used in the main query.

### Summary
- **Subqueries** allow for more complex SQL operations by nesting one query inside another.
- Subqueries can be used in the:
  1. `WHERE` clause to compare values with aggregate results.
  2. **Column expressions** to calculate or retrieve additional data.
  3. **FROM clause** as a **derived table** for more complex scenarios.
- These techniques enable you to write more powerful and efficient queries.
