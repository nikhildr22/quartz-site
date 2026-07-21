---
Created: 7th January 2023 05:36 AM
alias: [inner join, full outer join, left outer join, right outer join, cross join, cartesian]
Status: 
Medium: youtube 
Tags: [inbox, dotnet]
url: https://youtu.be/3t2X1jczt4g
links: 
---
___



# inner join
![[Pasted image 20230107053840.png]]
matching records from both tables
![[Pasted image 20230107053941.png]]
This is our data

![[Pasted image 20230107053932.png]]

![[Pasted image 20230107054024.png]]
we get only matching records from both the tables.


# left outer joins
![[Pasted image 20230107054114.png]]

![[Pasted image 20230107054138.png]]
how to identify which table is left which right? it is in the same order as mentioned in the query.

Left outer join returns all data from left table, and only matching records from right table.

# right outer join
its the mirror image of left outer join
![[Pasted image 20230107054342.png]]

![[Pasted image 20230107054426.png]]


# whats the using where clause in outer joins
![[Pasted image 20230107054528.png]]
we can identify the scenarios where the matching data dont exist.
when customers dont have coupons, when flights dont have planes

# full outer join

![[Pasted image 20230107054726.png]]
combining both left and right joins.
![[Pasted image 20230107054748.png]]

# cross joins
cartesian product obtained by multiplying number of rows in one table with the number of rows in another table.

why we meed it? we can generate a combination of all data. can be used for sample data generation.
![[Pasted image 20230107054909.png]]