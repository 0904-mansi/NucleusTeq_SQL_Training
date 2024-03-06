# Day 1 to 6

 1. [create table](#create-table)
 2. [SELECT Clause](#select-clause)
 3. [WHERE Clause](#where-Clause)
 4. [DELETE Clause](#delete-clause)
 5. [INSERT](#insert)
 6. [Drop and Truncate](#drop-truncate)
 7. [with](#with)
 8. [OFFSET-FETCH](#offset-fetch)
 9. [Aliases](#aliases)
 10. [Wildcard Operator](#wildcard)
 11. [ALTER (ADD, DROP, MODIFY)](#alter)
  
# Create table
 ## SQL CREATE TABLE Statement

A Table is a combination of rows and columns. For creating a table we have to define the structure of a table by adding names to columns and providing data type and size of data to be stored in columns.
Syntax:
```
CREATE table table_name
(
Column1 datatype (size),
column2 datatype (size),
.
.
columnN datatype(size)
);
```

## Example
```
CREATE TABLE Subject
(
Sub_ID INT, 
Sub_Name varchar(20)
);
```

# Add data to the Table

To add data to the table, we use INSERT INTO, the syntax is as shown below:
Syntax:
```
Insert into Table_name(Column1, Column2, Column3)
Values (Value1, value2, value3);
```

## Example

```
//Adding multiple data in the table in one go//
Insert into Subject
Values (1,'English'),
(2,'French'),
(2,'Science'),
(2,'Maths');

```
# Create a Table Using Another Table

Syntax:

```
CREATE TABLE new_table_name AS
    SELECT column1, column2,...
    FROM existing_table_name
    WHERE ....;
```


# Select clause

Select is the most commonly used statement in SQL. The SELECT Statement in SQL is used to retrieve or fetch data from a database. We can fetch either the entire table or according to some specified rules. 

To fetch the entire table or all the fields in the table:
```
 SELECT * FROM table_name; 
```

Example
```
SELECT column1,column2 FROM table_name 
column1 , column2: names of the fields of the table
table_name: from where we want to apply query
```
# WHERE Clause

WHERE keyword is used for fetching filtered data in a result set. It is used to fetch data according to a particular criteria. WHERE keyword can also be used to filter data by matching patterns.

## Basic Syntax: 

```
SELECT column1,column2 FROM table_name WHERE column_name operator value;
```
![image](https://user-images.githubusercontent.com/81081105/226430500-379b9fa9-1f6d-4a43-bf47-e055dbc6be36.png)

# BETWEEN operator

It is used to fetch filtered data in a given range inclusive of two values. Basic Syntax: SELECT column1,column2 FROM table_name WHERE column_name BETWEEN value1 AND value2;

To fetch records of students where ROLL_NO is between 1 and 3 (inclusive)
```
SELECT * FROM Student WHERE ROLL_NO BETWEEN 1 AND 3;
```

# LIKE operator

It is used to fetch filtered data by searching for a particular pattern in where clause. Basic Syntax: SELECT column1,column2 FROM table_name WHERE column_name LIKE pattern;

 To fetch records of students where NAME starts with letter S.
```
SELECT * FROM Student WHERE NAME LIKE 'S%'; 
```
The ‘%'(wildcard) signifies the later characters here which can be of any length and value.More about wildcards will be discussed in the later set

# IN operator

It is used to fetch filtered data same as fetched by ‘=’ operator just the difference is that here we can specify multiple values for which we can get the result set. Basic Syntax: SELECT column1,column2 FROM table_name WHERE column_name IN (value1,value2,..);

  To fetch NAME and ADDRESS of students where Age is 18 or 20.
```
SELECT NAME,ADDRESS FROM Student WHERE Age IN (18,20);
```

# DELETE clause

The DELETE Statement in SQL is used to delete existing records from a table. We can delete a single record or multiple records depending on the condition we specify in the WHERE clause.

Syntax: Basic 

DELETE FROM table_name WHERE some_condition;

# INSERT

The INSERT INTO statement of SQL is used to insert a new row/record in a table. There are two ways of using the INSERT INTO statement for inserting rows.

`
Syntax:

    INSERT INTO table_name (column1, column2, column3) 

    VALUES ( value1, value2, value3); 
    
    or 
    
    INSERT INTO table_name VALUES (value1, value2, value3); 
    
    
`

  inserting all columns of a table: We can copy all the data of a table and insert it into a different table.

Syntax:

    INSERT INTO first_table SELECT * FROM second_table;
    
# Drop Truncate

## DROP

DROP is used to delete a whole database or just a table.The DROP statement destroys objects like an existing database, table, index, or view. A DROP statement in SQL removes a component from a relational database management system (RDBMS). 

Syntax:
`
DROP object object_name

Examples:
DROP TABLE table_name;
table_name: Name of the table to be deleted.

DROP DATABASE database_name;
database_name: Name of the database to be deleted.
`

# DROP vs TRUNCATE

    Truncate is normally ultra-fast and its ideal for deleting data from a temporary table.
    Truncate preserves the structure of the table for future use, unlike drop table where the table is deleted with its full structure.
    Table or Database deletion using DROP statement cannot be rolled back, so it must be used wisely.

![image](https://user-images.githubusercontent.com/81081105/229492833-dbfb0810-35f9-4437-834a-53e07c9da09d.png)

Note :  A TRUNCATE TABLE statement can be rolled back in SQL Server by using a transaction but delete statement can't be roll back.

# With

1. The clause is used for defining a temporary relation such that the output of this temporary relation is available and is used by the query that is associated with the WITH clause.
2. Queries that have an associated WITH clause can also be written using nested sub-queries but doing so add more complexity to read/debug the SQL query.
3. WITH clause is not supported by all database system.
4. The name assigned to the sub-query is treated as though it was an inline view or table

Syntax: 
`
WITH temporaryTable (averageValue) as
    (SELECT avg(Attr1)
    FROM Table)
    SELECT Attr1
    FROM Table, temporaryTable
    WHERE Table.Attr1 > temporaryTable.averageValue;
`

# OFFSET-FETCH
OFFSET and FETCH Clause are used in conjunction with SELECT and ORDER BY clause to provide a means to retrieve a range of records.

## OFFSET

The OFFSET argument is used to identify the starting point to return rows from a result set. Basically, it exclude the first set of records.(it deletes number of rows mentioned with offset command)

Note:

    OFFSET can only be used with ORDER BY clause. It cannot be used on its own.
    OFFSET value must be greater than or equal to zero. It cannot be negative, else return error.
    
Syntax:
`
SELECT column_name(s)
FROM table_name
WHERE condition
ORDER BY column_name
OFFSET rows_to_skip ROWS;
`
## FETCH

The FETCH argument is used to return a set of number of rows. FETCH can’t be used itself, it is used in conjunction with OFFSET.
Syntax:
`
SELECT column_name(s)
FROM table_name
ORDER BY column_name
OFFSET rows_to_skip
FETCH NEXT number_of_rows ROWS ONLY;
`

# Aliases

Aliases are the temporary names given to table or column for the purpose of a particular SQL query. It is used when name of column or table is used other than their original names, but the modified name is only temporary.

1. Aliases are created to make table or column names more readable.
2. The renaming is just a temporary change and table name does not change in the original database.
3. Aliases are useful when table or column names are big or not very readable.
4. These are preferred when there are more than one table involved in a query.

Basic Syntax:

    For column alias:

    SELECT column as alias_name FROM table_name;
    column: fields in the table
    alias_name: temporary alias name to be used in replacement of original column name 
    table_name: name of table

# Wildcard

![image](https://user-images.githubusercontent.com/81081105/229745580-ef047193-8613-48b0-80fe-d178fd459578.png)

# Alter

The ALTER TABLE statement is used to add, remove, or modify columns in an existing table. The ALTER TABLE statement is also used to add and remove various constraints on existing tables.

# Like

![image](https://user-images.githubusercontent.com/81081105/229759927-0738dbde-7bda-4291-be68-5cf1dece04c4.png)

# Between

The SQL BETWEEN condition allows you to easily test if an expression is within a range of values (inclusive). The values can be text, date, or numbers. It can be used in a SELECT, INSERT, UPDATE, or DELETE statement. The SQL BETWEEN Condition will return the records where expression is within the range of value1 and value2. 

Syntax: 
 
`
   SELECT column_name(s)
   FROM table_name
   WHERE column_name BETWEEN value1 AND value2;
`

# IN

IN operator allows you to easily test if the expression matches any value in the list of values. It is used to remove the need of multiple OR condition in SELECT, INSERT, UPDATE or DELETE. You can also use NOT IN to exclude the rows in your list. We should note that any kind of duplicate entry will be retained. 
Syntax: 
 
`
SELECT column_name(s)
FROM table_name
WHERE column_name IN (list_of_values);
`

# Switch case

Sample Query:
Consider a variable, department_name which is entered in the SQL code.
`
CASE department_name
 WHEN 'CS'
  THEN UPDATE Faculty SET
  department='Computer Science';
 WHEN 'EC'
  THEN UPDATE Faculty SET
  department='Electronics and Communication';
 ELSE UPDATE Faculty SET
 department='Humanities and Social Sciences';
END CASE
`

# Aggregate-functions

