# Introduction to Relational Databases and Tables

## Relational Databases
- Is the database that is consitsted of tables.
- These tables can be linked to one another through keys.
- **Entity-Relationship Database** is the a model/framework used to design databases.
  - Entities: Are the tables
  - Attributes: are the data elements of that entity.
    - Proerties of that entry.

## Types of SQL statements (DDL vs DML)
- **DDL** or **Data Definition Language** is used to define, change or drop database objects like tables.
  - This is statements that affect the structure of the database not the data in the database.
- **DML** or **Data Manipulation Language** is used to modify and alter the data in the tables.
  - These do not affect the structure of the table or database.

## CREATE TABLE Statement

```sql
    CREATE TABLE tablename(
        col_name datatype PRIMARY KEY NOT NULL,
        col2_name datatype
    )
```

# ALTER, DROP, and TRUNCATE Tables in SQL

## Introduction

Hello and welcome to altering, dropping, and truncating tables. After going through this guide, you will be able to:

- Describe the `ALTER TABLE`, `DROP TABLE`, and `TRUNCATE TABLE` statements.
- Explain their syntax.
- Use these statements in SQL queries.

---

## ALTER TABLE Statement

The `ALTER TABLE` statement is used to:

- **Add or remove columns** from a table.
- **Modify the data type** of columns.
- **Add or remove keys**.
- **Add or remove constraints**.

### Syntax

```sql
ALTER TABLE table_name
    [ADD COLUMN column_name data_type]
    [MODIFY column_name new_data_type]
    [DROP COLUMN column_name];
```
- Start with `ALTER TABLE` followed by the name of the table you want to alter.
- Unlike the `CREATE TABLE` statement, you do not use parentheses to enclose parameters.
- Each clause in the `ALTER TABLE` statement specifies one change you want to make to the table.

## Examples
### Adding a Column

To add a `telephone_number` column to the `author` table in the library database to store the authors' telephone numbers:

```sql
ALTER TABLE author
ADD COLUMN telephone_number BIGINT;
```
-     In this example, the data type `BIGINT` is used, which can hold a number up to 19 digits long.

### Modifying a Column's Data Type

Using a numeric data type for `telephone_number` means you cannot include characters like parentheses, plus signs, or dashes. To overcome this, you can change the column to use the `CHAR` data type.

To modify the data type of the `telephone_number` column:

```sql
ALTER TABLE author
MODIFY telephone_number CHAR(20);
```

- Caution: Altering the data type of a column containing existing data can cause problems if the existing data is not compatible with the new data type.
    - For example, changing a column from the `CHAR` data type to a numeric data type will not work if the column already contains non-numeric data.
    - Attempting this will result in an error message in the notification log, and the statement will not run.

### Dropping a Column

If your specifications change and you no longer need an extra column, you can remove it using the `DROP COLUMN` clause.

To remove the `telephone_number` column from the `author` table:
```sql
ALTER TABLE author
DROP COLUMN telephone_number;
```

## DROP TABLE Statement

The `DROP TABLE` statement is used to delete an entire table from a database.

**Important**: If you delete a table that contains data, the data will be deleted alongside the table by default.

### Syntax

```sql
DROP TABLE table_name;
```
### Example

To remove the author table from the database:

```sql
DROP TABLE author;
```

## TRUNCATE TABLE Statement

Sometimes you might want to delete all the data in a table without deleting the table itself. While you can use the `DELETE` statement without a `WHERE` clause to do this, it is generally quicker and more efficient to truncate the table instead.

The `TRUNCATE TABLE` statement deletes all rows in a table but keeps the table structure intact.
### Syntax

```sql
TRUNCATE TABLE table_name IMMEDIATE;
```
The `IMMEDIATE` keyword specifies to process the statement immediately and that it cannot be undone.
### Example

To truncate the `author` table:

```sql
ALTER TABLE author
TRUNCATE TABLE author IMMEDIATE;
```
