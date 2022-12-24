---
title: Basic SQL Queries
tags: [SQL]
---
SQL stands for Structured Query Language which is a RDB(Relational Database). SQL lets you access and manipulate databases. Some basic SQL queries are given below:

### SELECT
The SELECT statement is used to select data from a database.
The data returned is stored in a result table, called the result-set.

Syntex
```sql
SELECT column1, column2, ...
FROM table_name;
```
Example 1
```sql
SELECT CustomerName, City FROM Customers;
```
Example 2
```sql
SELECT * FROM Customers;
```

### SELECT DISTINCT
The SELECT DISTINCT statement is used to return only distinct (different) values.
Inside a table, a column often contains many duplicate values; and sometimes you only want to list the different (distinct) values.

Syntex
```sql
SELECT DISTINCT column1, column2, ...
FROM table_name;
```
Example 1
```sql
SELECT DISTINCT Country FROM Customers;
```

The following SQL statement lists the number of different (distinct) customer countries.

Example 2 (Doesn't work on MS Access)
```sql
SELECT COUNT(DISTINCT Country) FROM Customers;
```

Example 3 (For MS Access)
```sql
SELECT Count(*) AS DistinctCountries
FROM (SELECT DISTINCT Country FROM Customers);
```

### WHERE
The WHERE clause is used to filter records.
It is used to extract only those records that fulfill a specified condition.

Syntex
```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition;
```
Example 1
```sql
SELECT * FROM Customers
WHERE Country='Mexico';
```
Example 2
```sql
SELECT * FROM Customers
WHERE CustomerID=1;
```
Operators in The WHERE Clause

| Operator | Description |
| :--- | :--- |
| =	| Equal	| 
| >	| Greater than	| 
| <	| Less than	| 
| >=	| Greater than or equal	| 
| <=	| Less than or equal	| 
| <>	| Not equal. Note: In some versions of SQL this operator may be written as !=	| 
| BETWEEN	| Between a certain range	| 
| LIKE	| Search for a pattern	| 
| IN	| To specify multiple possible values for a column| 

### AND, OR and NOT
The WHERE clause can be combined with AND, OR, and NOT operators. The AND and OR operators are used to filter records based on more than one condition:

- The AND operator displays a record if all the conditions separated by AND are TRUE.
- The OR operator displays a record if any of the conditions separated by OR is TRUE.

The NOT operator displays a record if the condition(s) is NOT TRUE.

AND Syntex
```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition1 AND condition2 AND condition3 ...;
```
OR Syntex
```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition1 OR condition2 OR condition3 ...;
```
AND Syntex
```sql
SELECT column1, column2, ...
FROM table_name
WHERE NOT condition;
```
Example 1
```sql
SELECT * FROM Customers
WHERE Country='Germany' AND City='Berlin';
```
Example 2
```sql
SELECT * FROM Customers
WHERE City='Berlin' OR City='München';
```
Example 3
```sql
SELECT * FROM Customers
WHERE NOT Country='Germany';
```
Example 4
```sql
SELECT * FROM Customers
WHERE Country='Germany' AND (City='Berlin' OR City='München');
```
Example 5
```sql
SELECT * FROM Customers
WHERE NOT Country='Germany' AND NOT Country='USA';
```

### ORDER BY
The ORDER BY keyword is used to sort the result-set in ascending or descending order.
The ORDER BY keyword sorts the records in ascending order by default. To sort the records in descending order, use the DESC keyword.

Syntax
```sql
SELECT column1, column2, ...
FROM table_name
ORDER BY column1, column2, ... ASC|DESC;
```
Example 1
```sql
SELECT * FROM Customers
ORDER BY Country;
```
Example 2
```sql
SELECT * FROM Customers
ORDER BY Country DESC;
```
Example 3
```sql
SELECT * FROM Customers
ORDER BY Country, CustomerName;
```
Example 4
```sql
SELECT * FROM Customers
ORDER BY Country ASC, CustomerName DESC;
```

### INSERT INTO
The INSERT INTO statement is used to insert new records in a table.<br>
It is possible to write the INSERT INTO statement in two ways:

- Specify both the column names and the values to be inserted
- Adding values for all the columns of the table

Syntex for specified columns and values
```sql
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);
```
Syntex for all columns
```sql
INSERT INTO table_name
VALUES (value1, value2, value3, ...);
```
Example 1
```sql
INSERT INTO Customers
VALUES (null, 'Cardinal', 'Tom B. Erichsen', 'Skagen 21', 'Stavanger', '4006', 'Norway');
```
Example 2
```sql
INSERT INTO Customers (CustomerName, City, Country)
VALUES ('Cardinal', 'Stavanger', 'Norway');
```

### NULL
It is not possible to test for NULL values with comparison operators, such as =, <, or <>. We will have to use the IS NULL and IS NOT NULL operators instead.

IS NULL Syntex
```sql
SELECT column_names
FROM table_name
WHERE column_name IS NULL;
```
IS NOT NULL Syntex
```sql
SELECT column_names
FROM table_name
WHERE column_name IS NOT NULL;
```
Example 1
```sql
SELECT CustomerName, ContactName, Address
FROM Customers
WHERE Address IS NULL;
```
Example 2
```sql
SELECT CustomerName, ContactName, Address
FROM Customers
WHERE Address IS NOT NULL;
```

### UPDATE
The UPDATE statement is used to modify the existing records in a table.

Syntex
```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```
Example 1
```sql
UPDATE Customers
SET ContactName = 'Alfred Schmidt', City= 'Frankfurt'
WHERE CustomerID = 1;
```
Example 2
```sql
UPDATE Customers
SET ContactName='Juan'
WHERE Country='Mexico';
```

### DELETE
The DELETE statement is used to delete existing records in a table.

Syntex
```sql
DELETE FROM table_name WHERE condition;
```
Syntex for deleting all content in the table while keeping the structure
```sql
DELETE FROM table_name;
```
Example 1
```sql
DELETE FROM Customers WHERE CustomerName='Alfreds Futterkiste';
```
Example 2
```sql
DELETE FROM Customers;
```

Happy Coding!