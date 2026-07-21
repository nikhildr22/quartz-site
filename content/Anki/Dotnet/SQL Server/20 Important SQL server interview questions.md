
---
Created: 19th December 2022 09:40 AM
alias: [database, sql server, interview]
Status: 
Medium: 
Tags: [inbox, dotnet, sql, ankied ]
url: https://youtu.be/SEdAF8mSKS4
links: test
---
___
ENDanki

STARTanki
Basic
# 3 P's of interview preparation?
Back:

Tips:
![[Pasted image 20221219100134.png]]
1. answer briefly and to the point.
2. preparation is the key
	1. ![[Pasted image 20221219100055.png]]

3. ![[Pasted image 20221219100112.png]]

>Be to the Point
>Be Prepared
>Be Practical
<!--ID: 1672019957373-->
ENDanki

START
Basic
# Explain Normalization ?
Back:

Normalization is a database design technique to remove redundant data.


END

STARTanki
Basic
# How to implement normalization ?
Back:

Normalization is implemented by splitting tables in to two , one with reference data ( master table) and other transaction data.
![[Pasted image 20221225083635.png]]
![[Pasted image 20221225083645.png]]
<!--ID: 1672019957395-->
ENDanki

STARTanki
Basic
# What is denormalization .
Back:


Denormalization is a database design technique to improve search performance.
We merge tables. Duplicate data is present in denormalization,


![[Pasted image 20221219100256.png]]

![[Pasted image 20221219100306.png]]
<!--ID: 1672019957407-->
ENDanki

STARTanki
Basic
# Explain OLTP vs OLAP ?
Back:

OLTP :- Online Transaction Processing
OLAP :- Online Analytical Processing.


==its related to normalization and denormalization.==
**OLTP** Normalization avoids redundancy and we follow normalization design(1st,2nd and 3rd normal).
**OLAP** Denormalization improve search performance and we follow denormalization design.

![[Pasted image 20221219100416.png]]
![[Pasted image 20221219100432.png]]



-----
<!--ID: 1672019957418-->
ENDanki

STARTanki
Basic
# Explain 1st,2nd and 3rd Normal form  ? (Hint: APT)
Back:

![[Pasted image 20221219100909.png]]
1st normal form :- A table is in first normal form when the columns have Atomic values. It should not have repeating groups.
Values should be ==atomic==
example:
before 1NF: ![[Pasted image 20221225084453.png]]

without 1NF we've to write these complex conversions to read and write fullname:
![[Pasted image 20221219100611.png]]

After 1NF: ![[Pasted image 20221225084546.png]]


2NF:
First normal form should be satisfied.
==All non-key columns should be full dependent on the Primar key==.
There should be no ==Partial dependancy==
![[Pasted image 20221226062348.png]]


the above form, the coutry is dependant on both Id and countryId, but for 2NF, all columns should be completely dependant on primary key.
![[Pasted image 20221226062405.png]]


3NF:
3rd Normal :- All 1st and 2nd normal form should be satisfied.
No ==transient depedency== should be present.
Transient  = No non-key column dependant on other non key column.
here, the `per cost` is dependant  on the `product` column
![[Pasted image 20221226062441.png]]
![[Pasted image 20221226065902.png]]
<!--ID: 1672019957430-->
ENDanki

STARTanki
Basic
# Primary Key vs Unique key ?
Back:

Remember the 2 Ns.
1. 1st N ==NULLS== :- Unique can have NULLS , but primary key can not have NULLS.
2. 2nd N ==Numbers== :- Many unique keys but ony ONE Primary key column in a table.
<!--ID: 1672019957442-->
ENDanki

STARTanki
Basic
# Differentiate between Char vs Varchar ?
Back:

- fixed vs varchar
- Char is Fixed length while
- varchar is variable length.
<!--ID: 1672019957454-->
ENDanki

STARTanki
Basic
# Differentiate between Char vs NChar ?
Back:

- If you want to just store english characters then use
- Char , For multilingual language (Non-English) use NChar.
- Char 1 Character = 1 byte
- NChar 1 Character = 2 bytes.
<!--ID: 1672019957465-->
ENDanki

STARTanki
Basic
# What is the use of Index ?
Back:

**Indexes increases search performance.**

==balanced tree== structure is created for the searching when we use indexing.
<!--ID: 1672019957477-->
ENDanki

STARTanki
Basic
# How does Indexing make search faster?
Back:

Search becomes faster because of Balance tree structure. 
lnternally it creates Node and Leaf nodes to reach to the data quick.
<!--ID: 1672019957488-->
ENDanki

STARTanki
Basic
# What are the two types of Indexes ? and Difference between them?
Back:

1. Clustered Index 
2. Non-Clustered Indexes.

Both will have ==balanced tree== structure.
Differences:
- In Clustered index leaf node will point to actual data. 
- While in case of non-clustered index leaf node takes help of clustered index
![[Pasted image 20221219104037.png]]
<!--ID: 1672019957501-->
ENDanki

STARTanki
Basic
# Function vs Stored Procedures in MSSQL
Back:
 doubt
- Function returns Computed Scalar values. **You can not make permanent changes(insert,update,delete) inside function**.
- Stored procedure is a mini-programs which can do anything , make changes , backup database.
![[Pasted image 20221219104309.png]]
![[Pasted image 20221219104417.png]]
<!--ID: 1672019957512-->
ENDanki

STARTanki
Basic
# What are triggers and why do you need it ?
Back:


Triggers are logics which can be executed when events like insert,update,delete etc happens.
![[Pasted image 20221219104455.png]]
<!--ID: 1672019957523-->
ENDanki

STARTanki
Basic
# What are 2 types of triggers ? difference, when to use, code examples?
Back:

There are two types:
1. **After** trigger  
2. **Instead OF** trigger.
After trigger :- After event has happened logic is executed.
Instead Of trigger:- Instead of the event the logic is executed.
==instead of==  trigger can be used to skip the actual behavior and do custom logic.
in the above example, the trigger will prevent the insert,delete and update operations on the table.

![[Pasted image 20221219104552.png]]
## AFTER Trigger
```sql
USE [customerDBEF]
GO
ALTER TRIGGER [dbo] . [trg_datamanipulation]
	ON [dbo] . [tb1Customer]
	after
		INSERT, DELETE,UPDATE
	AS
BEGIN
	insert into tb1Audit(Lastupdated) values(Getdate())
END
```
## INSTEAD OF trigger-
```sql
USE [CustomerDBEF]
GO
ALTER TRIGGER [dbo]. [trg_datamanipul.
	ON [dbo] . [tbICustomer]
	instead of
		INSERT, DELETE,UPDATE
	AS
BEGIN
	insert into tbIAudit(Lastupdated) values(Getdate())
END
```
<!--ID: 1672019957535-->
ENDanki

STARTanki
Basic
# What is need of Identity ?
Back:

Identity helps to define auto-incremented column.
<!--ID: 1672019957548-->
ENDanki

STARTanki
Basic
# Explain transactions and how to implement it ?
Back:

Transaction helps to implement series of activity treat as one single unit. Either everything is successful and or everything rollbacks.
```sql
begin try
begin tran
	insert into tb1Customer(FirstName) values( 'Shivl')
	insert into tb1Customer FirstName values( 'Shiv2')
	--delete
	--update I
commit tran
end try
begin catch
	rollback
```
<!--ID: 1672019957558-->
ENDanki

STARTanki
Basic
# What are inner joins ?
Back:

Inner join selects matching records from both tables.
<!--ID: 1672019957569-->
ENDanki

STARTanki
Basic
# What are inner joins ?
Back:

Inner join selects matching records from both tables.
![[Pasted image 20221226063537.png]]



]]![[Pasted image 20221219105209.png]]
<!--ID: 1672112230492-->
ENDanki

STARTanki
Basic
# Explain Left join ?
Back:

All data from left table selected and only matching records from right table.

![[Pasted image 20221219105240.png]]
<!--ID: 1672019957584-->
ENDanki

STARTanki
Basic
# Explain Right join ?
Back:

All data from right table selected and only matching records from left table.
```SQL
select FirstName, CountryCode from tb1Customer
right join mst_Country on tb1Customer.CountryId = mst_Country.ld
```
![[Pasted image 20221226064328.png]]
<!--ID: 1672019957594-->
ENDanki

STARTanki
Basic
# Explain Full outer joins ?
Back:

All matching and unmatching records from both left and right table are selected.
```sql
select FirstName,CountryCode from tb1Customer 
full outer join mst_Country
on tb1Customer.CountryId = mst_Country.Id
```
![[Pasted image 20221226064011.png]]
<!--ID: 1672019957604-->
ENDanki

STARTanki
Basic
# Explain Cross joins ?
Back:
So the rule to remember is:

> **CROSS JOIN combines entire rows, not individual columns.** The number of **rows** is multiplied (`m × n`), while the number of **columns** is simply the sum of the selected columns from both tables.


Cross join is cartesian. Every record of one table is joined with other table records.
we cant use `ON` Keyword on Cross Joins.
![[Pasted image 20221226064439.png]]

![[Pasted image 20221219105338.png]]
cartesian product - aka all possible records.
<!--ID: 1672019957615-->
ENDanki


STARTanki
Basic
# What are inner joins ?
Back:

Inner join selects matching records from both tables.

ENDanki

STARTanki
Basic
# Explain Left join ?
Back:

All data from left table selected and only matching records from right tabl
<!--ID: 1672112230523-->
ENDanki

STARTanki
Basic
# Explain Right join ?
Back:

All data from right table selected and only matching records from left tabl
<!--ID: 1672112230542-->
ENDanki

STARTanki
Basic
# Explain Full outer joins ?
Back:

All matching and unmatching records from both left and right table are
selected.
<!--ID: 1672112230560-->
ENDanki

STARTanki
Basic
# Explain Cross joins ?
Back:

Cross join is cartesian. Every record of one table is joined with other table
records.
<!--ID: 1672112230578-->
ENDanki


