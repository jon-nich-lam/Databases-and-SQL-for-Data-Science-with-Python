# Basic of Sql

## Introduction to Database
- **SQL** is a language used for relational database and uised to query data
  - Short for Structured Query Language
- **Database** is a repository of data.
  - **Tabular Database** is where the data is stored in tables like a spreadsheet.
    - This is where columns and rows exists which is also a relational database.
- **DBMS** or Database management system is a set of software tools for the data in the database.
- **RDBMS** is a relational database management system
  - Examples of RDBMS are:

    1. MySQL
    2. Oracle Database
    3. DB2
- The most simplest and most used commands for databases are:
    1. Create a table
    2. Insert data into a table
    3. Select data from a table
    4. Update data in a table
    5. Delte data in a table

## Select Statement
- **Select** is a **Data Manipulation Language** statement
  - **Data Manipulation Langage** or DML are used to read or modify data
- The most simplest example of select is to select all entries in a table

```sql
    SELECT * from <tablename>
```

If you want to specify specific columns you can specify which columns instead of the *

```sql
    SELECT column1, column3 from tablename
```

The order of the columns displayed will match the order of the select statement.

- Instead of getting all entries what if we want to query for a specific value in a column?

### Where clause
- This is where the **WHERE** clause comes into play
- The WHERE clause requires a **predicate**
  - **Predicate** is a statement that evaluates to True, False or Unknown.

Lets say we want to search for the title and book_id the Book table where the title is Robin Hood

```sql
    SELECT title, book_id FROM book WHERE title='Robin Hood' 
```

All comparison operators are what they normally are except for not equal to which is **<>**

### Count, Distinct, Limit
- These are all used with the Select Statement

- **Count**: is used to return the number of rows that match the query

```sql
    SELECT COUNT(COUNTRY) FROM Medals where COUNTRY='Canada'
```
- **Distinct** : is used to retrieve unique entries from the rows
  - For example lets say we have multiple entries from the same country that has won gold and we wanted to find which countries have won gold. We don't need to duplicate the same country.

```sql
    SELECT DISTINCT COUNTRY FROM Medals where MEDALTYPE='GOLD'
```

- **Limit** : Is used to restrict the number of rows in a database

```sql
    SELECT * FROM Medal WHERE YEAR=2018 LIMIT 5
```

- **Offset** : can be used with Limit to view data after a certain offsett

## Insert Statement
- **Insert** is used to add data to a table
    - To insert we follow the format of the following
```sql
    INSERT INTO Tablename (ColumnName,...) VALUES (InputValues,...)
```
Here is an example of inputting an Author entry
``` sql
    INSERT INTO Author (AUTHOR_ID, LASTNAME, FIRSTNAME, EMAIL, CITY, COUNTRY) VALUES ('A1', 'Lam', 'Jonathan', 'Test@gmail.com', 'San Francisco', 'CA')
```

Multiple rows can be inserted for Values

``` sql
    INSERT INTO Author (AUTHOR_ID, LASTNAME, FIRSTNAME, EMAIL, CITY, COUNTRY) VALUES ('A1', 'Lam', 'Jonathan', 'Test@gmail.com', 'San Francisco', 'CA'),
    ('A2', 'Smith', 'Will', 'Test2@gmail.com', 'Seattle', 'WA')
```

## Update and Delete
- **Update** : Read and Modify data. The syntax goes as follow

```sql
    UPDATE tableName SET [columnName = Value] <WHERE CONDITION>
```
Here is a practical use

```sql
    UPDATE AUTHOR SET LastName = 'Smith' Firstname = 'Will' WHERE AuthorID ='A2'
```

- If you don't specify the Where clause All rows will be updated.
- **Delete** is used to delete entry. The Syntax goes as follow
```sql
    DELETE FROM tablename WHERE Condition
```

Here is a practical use

```sql
    DELETE FROM Author WHERE Author_ID in ('A2','A3')
```