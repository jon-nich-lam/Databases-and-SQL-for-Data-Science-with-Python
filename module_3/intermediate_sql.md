
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

## Summary
- **DISTINCT** removes duplicate values from a result set.
- **GROUP BY** groups rows that have the same values in specified columns.
- **HAVING** filters groups based on conditions, often using aggregate functions like `COUNT`.
- You can use **AS** to rename calculated columns for clarity.
