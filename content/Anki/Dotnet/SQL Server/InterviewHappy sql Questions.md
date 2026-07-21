
---
Created: 28th December 2022 03:01 AM
alias: [sql server, mssql]
Status: 
Medium: youtube 
Tags: [inbox, dotnet, ankied ]
url: https://youtu.be/034DqhbCboo
links: 
---
___
ENDanki

STARTanki
Basic
# InterviewHappy sql  basics Questions
Back:

Q. What is the difference between DBMS and RDBMS?
Q. What is a Constraint is SQL? What are its types.
Q. What is the difference between Primary key and
Unique key?
Q. What are Triggers and types of triggers?
Q. What is a View?
Q. What is the difference between Having clause and
Where clause?
Q. What is Sub query or Nested query or Inner query in
SQL?
Q. What is Auto Increment/ Identity column in SQL
Server?
<!--ID: 1672266716598-->
ENDanki

STARTanki
Basic
# What is the difference between DBMS and RDBMS?
Back:

| DBMS                                 | RDBMS                                                                                               |
| ------------------------------------ | --------------------------------------------------------------------------------------------------- |
| 1. DBMS stores data as file.         | RDBMS stores data in TABULAR form.                                                                  |
| 2. No relationship between data      | Data is stored in the form of tables which are RELATED to each other. Eg: Foreign key relationship. |
| Normalization is not present.        | NORMALIZATION is present.                                                                           |
| It deals with small quantity of data | It deals with LARGE amount of data.                                                                 |
| Examples: XML                        | Examples: MySQL, PostgreSQL, SQL Server, Oracle   ,Microsoft Access etc.                                                                                                 |
<!--ID: 1672266716605-->
ENDanki

STARTanki
Basic
# What is a Constraint is SQL? What are its 6 types.
Back:

SQL constraints are used to specify rules for the data in a table.
Constraints are used to limit the type of data that can go into a table.
1. Primary Key
2. Not Null
3. foreign key
4. check
5. default
6. unique
![[Pasted image 20221228053329.png]]
<!--ID: 1672266716609-->
ENDanki

STARTanki
Basic
# What is the difference between Primary key and Unique key?
Back:

![[Pasted image 20221228030648.png]]
<!--ID: 1672266716613-->
ENDanki

STARTanki
Basic
# What are Triggers and types of triggers?
Back:

Triggers are stored programs, which are AUTOMATICALLY executed or fired when some events (insert, delete and update) occur.
The trigger runs **only once**.

Inside every INSERT trigger, SQL Server creates a temporary table called `INSERTED`

```sql
CREATE TRIGGER trg_Insert
ON Employee
AFTER INSERT
AS
BEGIN
    SELECT *
    FROM INSERTED;
END;
```


For UPDATE trigger SQL Server provides 2 temp tables:
```sql
CREATE TRIGGER trg_UpdateEmployee
ON Employee
AFTER UPDATE
AS
BEGIN
    SELECT
        d.Salary AS OldSalary,
        i.Salary AS NewSalary
    FROM INSERTED i
    JOIN DELETED d
        ON i.Id = d.Id;
END;
```

![[Pasted image 20221228030807.png]]
An INSTEAD OF trigger is a trigger that allows you to skip an
INSERT , DELETE , or UPDATE statement to a table or a view and
execute other statements defined in the trigger instead.
![[Pasted image 20221228030904.png]]

![[Pasted image 20221228030820.png]]
<!--ID: 1672266716618-->
ENDanki

STARTanki
Basic
# What is a View in SQL Server?
Back:

A view is a VIRTUAL table which consists of a subset of data contained in a table or more than one table.

Normally you'd write:
```sql
SELECT
    e.Name,
    d.Department
FROM Employee e
JOIN Department d
ON e.DepartmentId = d.Id;
```


Instead, save it:
```sql

CREATE VIEW EmployeeDepartmentView
AS
SELECT
    e.Name,
    d.Department
FROM Employee e
JOIN Department d
ON e.DepartmentId = d.Id;
```

Now anyone can simply do:

```sql
SELECT *
FROM EmployeeDepartmentView;
```



![[Pasted image 20221228031044.png]]
<!--ID: 1672266716623-->
ENDanki

STARTanki
Basic
# What is the difference between Having clause and Where clause?
Back:

WHERE Clause is used before GROUP BY Clause.
HAVING Clause is used after GROUP BY Clause.

WHERE Clause cannot contain AGGREGATE function.
HAVING Clause can contain aggregate function.
![[Pasted image 20221228053531.png]]
<!--ID: 1672266716628-->
ENDanki

STARTanki
Basic
# What is Sub query or Nested query or Inner query in SQL?
Back:

A Subquery or Inner query or a Nested query is a query
within another SQL query and embedded within the
WHERE clause.
![[Pasted image 20221228031217.png]]
<!--ID: 1672266716632-->
ENDanki

STARTanki
Basic
# What is Auto Increment/ Identity column in SQL Server?
Back:

Auto-increment allows a unique number to be
generated automatically when a new record is
inserte Into a table.
Mostly it is the primary key only.
![[Pasted image 20221228031301.png]]
<!--ID: 1672266716637-->
ENDanki

STARTanki
Basic
# Joins QUESTIONS
Back:

Q. What are Joins in SQL?
Q. What are the types of Joins in SQL Server?
Q. What is Self-Join?
Q. Write a SQL query to fetch all the Employees
who are also Managers.
<!--ID: 1672266716642-->
ENDanki

STARTanki
Basic
# What are Joins in SQL?
Back:

A join clause is used to COMBINE rows from two or more tables, based on a related column between them.
![[Pasted image 20221228031413.png]]
<!--ID: 1672266716646-->
ENDanki

STARTanki
Basic
# What are the types of Joins in SQL Server? (4 types)
Back:

1. Left outer Join
2. Right Outer join
3. Inner Join
4. Full outer Join
![[Pasted image 20221228031521.png]]
<!--ID: 1672266716651-->
ENDanki

STARTanki
Basic
# What is Self-Join? and when to use it? give an example scenario.
Back:

A self join is a join of a table to itself.
![[Pasted image 20221228031647.png]]
<!--ID: 1672266716656-->
ENDanki

STARTanki
Basic
# Write a SQL query to fetch all the Employees who are also Managers.
Back:
#doubt can we use self join?
![[Pasted image 20221228031751.png]]
<!--ID: 1672266716660-->
ENDanki

STARTanki
Basic
# indexes questions
Back:

Q. What are Indexes in SQL Server?
Q. What is Clustered index?
Q. What is Non-Clustered index?
Q. What is the difference between Clustered and Non-
Clustered index?
Q. How to create Clustered and Non-Clustered index in
a table?
Q. In which column you will apply the indexing to
optimize this query. "select id, class from student where
name="happy
<!--ID: 1672266716665-->
ENDanki

STARTanki
Basic
# What are Indexes in SQL Server?
Back:

SQL Indexes are used in relational databases to retrieve data VERY FAST.
They are similar to indexes at the start of the BOOKS, which purpose is to find a topic quickly.
![[Pasted image 20221228053950.png]]
<!--ID: 1672266716669-->
ENDanki

STARTanki
Basic
# What is Clustered index? what is default clustered index in SQL server?
Back:

CLUSTERED INDEX
- A clustered index defines the order in which data is physically stored in a table.
- Table data can be sorted in only way, therefore, there can be only one clustered index per table.
- In SQL Server, if you set a **primary key** on a column then it will automatically creates a clustered index on that particular column.
<!--ID: 1672266716674-->
ENDanki

STARTanki
Basic
# What is Non-Clustered index?
Back:

NON-CLUSTERED INDEX
A non-clustered index is stored at one place and table data is stored in another place. So this index is not physically stored.

A table can have multiple non-clustered index in a table.
![[Pasted image 20221228113057.png]]
<!--ID: 1672266716679-->
ENDanki

STARTanki
Basic
# What is the difference between Clustered and Non-Clustered index?
Back:

1. A clustered index defines the order in which data is physically stored in a table. For example Dictionary.
	 A non-clustered index is stored at one place and table data is stored in another place. For example Book Index.
2. A table can have only one clustered index.
	A table can have multiple non-clustered index.

3. Clustered index is faster.
	Non-clustered index is slower.

![[Pasted image 20221228113303.png]]
<!--ID: 1672266716683-->
ENDanki

STARTanki
Basic
# How to create Clustered and Non-Clustered index in a table?
Back:

CLUSTERED INDEX
When you create a PRIMARY KEY constraint, a clustered index on the columns is automatically created.
![[Pasted image 20221228113403.png]]
```sql
CREATE CLUSTERED INDEX ix_parts_id
ON production.parts (part_id);  
```
![[Pasted image 20221229063659.png]]
## Non-Clustered Index:
![[Pasted image 20221228113324.png]]
<!--ID: 1672266716687-->
ENDanki

STARTanki
Basic
# In which column you will apply the indexing to optimize this query. `select id, class from student where name='happy'`?
Back:

```sql

select id, class from student
Where name='happy'
```


The column after WHERE condition, which is "NAME"  in above statement.
<!--ID: 1672266716690-->
ENDanki

STARTanki
Basic
# stored procedures & functions and others
Back:

Q. What is the difference between Stored Procedure and
Functions (at least 3)?
Q. How to optimize a Stored Procedure or SQL Query?
Q. What is a Cursor? Why to avoid them?
Q. What is the difference between scope_identity and
@@identity?
Q. What is CTE in SQL Server?
Q. What is the difference between Delete, Truncate and Drop
commands?
Q. How to get the Nth highest salary of an employee?
Q. What are ACID properties?
Q. What are Magic Tables in SQL Server?
<!--ID: 1672266716695-->
ENDanki

STARTanki
Basic
# What is the difference between Stored Procedure and Functions (at least 3)?
Back:

memorize atleast 3
1. SP may or may not return a value but function must return a value.
2. SP can have input/output parameters but function only has input parameters.
3. We can call function inside SP but cannot call SP from a function.
4. We cannot use SP in SQL statements like SELECT, INSERT, UPDATE, DELETE, MERGE, etc. but we can use them with function.
	1. `SELECT *, dbo.fnCountry(city.long) FROM city;`  `
5. We can use try-catch exception handling in SP but we cannot do that in function.
6. We can use transactions inside SP but it is not possible in function. 
```sql
—Stored Procedure
CREATE PROCEDURE proc_name
(@Ename varchar(50),
BEGIN
INSERT INTO Employee (EmpName) VALUES (@Ename)
SELECT
END
 
—UDF — User Defined Functions
CREATE FUNCTION function_name (parameters)
—only input parameter
RETURNS data_type AS
BEGIN
	SQL statements
	RETURN value
END;
```
<!--ID: 1672266716699-->
ENDanki

STARTanki
Basic
# How to optimize a Stored Procedure or SQL Query? (6 points)
Back:

1. Use SET NOCOUNT ON
	1. ![[Pasted image 20221229035315.png]]
2. Specify column names instead of using * in SELECT statement.
3. Use schema name before objects or tablenames. Example: SELECT EmplD, Name FROM dbo.Employee
4. Do not use DYNAMIC QUERIES. They are vulnerable to SQL Injections.
5. Use EXISTS instead of COUNT ().
	- Example :SELECT Count(l) FROM db0.Employee
	- Example: EXISTS (SELECT 1 FROM db.Employees))
6. Use TRANSACTION when required only
<!--ID: 1672266716703-->
ENDanki

STARTanki
Basic
# What is a Cursor? Why to avoid them? (DOFCD)
Back:

A database Cursor is a control which enables traversal/ iteration over the rows or records in the table.
5 step process:
1. Declare
2. Open
3. Fetch using while loop
4. Close
5. Deallocate
LIMITATION
A cursor is a MEMORY resident set of pointers -- meaning it occupies lots of memory from your system which is not good for performance.

![[Pasted image 20221229035604.png]]
<!--ID: 1672266716707-->
ENDanki

STARTanki
Basic
# What is the difference between scope_identity and @@identity?
Back:

Both are used to get the last value entered in the identity column of
The @@identity returns the last identity created in the same session. The session is the database connection.
`SELECT @@IDENTITY`

The scope_identity() function returns the last identity created in the same session and the same scope. The scope is the current query or the current stored procedure.
`SELECT SCOPE_IDENTITY()`

Normally we have to use scope_identity() function inside stored procedures.
<!--ID: 1672266716710-->
ENDanki

STARTanki
Basic
# What is CTE in SQL Server?
Back:

A Common Table Expression, is a TEMPORARY named result set, that you can reference within a `SELECT, INSERT, UPDATE, or DELETE` statement.
![[Pasted image 20221229035919.png]]
<!--ID: 1672266716714-->
ENDanki

STARTanki
Basic
# What is the difference between Delete, Truncate and Drop commands?
Back:

![[Pasted image 20221228033054.png]]
<!--ID: 1672266716718-->
ENDanki

STARTanki
Basic
# How to get the Nth highest salary of employee table?
Back:

![[Pasted image 20221228033214.png]]
<!--ID: 1672266716722-->
ENDanki

STARTanki
Basic
# What are ACID properties?
Back:

![[Pasted image 20221228033309.png]]
<!--ID: 1672266716726-->
ENDanki

STARTanki
Basic
# What are Magic Tables in SQL Server?
Back:

![[Pasted image 20221228033408.png]]
<!--ID: 1672266716730-->
ENDanki

