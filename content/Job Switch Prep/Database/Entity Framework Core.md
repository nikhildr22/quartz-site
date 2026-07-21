---
Created: 4th November 2022 10:29 AM
alias: [EF Core, Best practices]
Status: 
Medium: 
Tags: [inbox, dotnet, todo/anki ]
url: https://youtu.be/qkJ9keBmQWo
links: 
---
___
  
# Entity Framework Best Practices


![[Pasted image 20221223043804.png]]
![[Pasted image 20221223043804.png]]

![[Pasted image 20221223043822.png]]

# adding a class library
![[Pasted image 20221223043919.png]]
here we are choosing this one because, at the time of recording video, .net standard class library was compatible with all other type of projects.
![[Pasted image 20221223044043.png]]

Add models in dataaccess layer
![[Pasted image 20221223044429.png]]
![[Pasted image 20221223045250.png]]

![[Pasted image 20221223045322.png]]
![[Pasted image 20221223045505.png]]
install this package in dataaccess layer.

create dataaccess class
add peopleContext class
![[Pasted image 20221223045614.png]]
![[Pasted image 20221223045635.png]]

to use this EF in our front end:
![[Pasted image 20221223045726.png]]
add a reference.

and in confgireservices, we need to add our dbcontetx class.

![[Pasted image 20221223045823.png]]

we can see that this `options.UseSQLServer` require EF core.
But now due to reference, even our frontend have EFCore nuget package.

## connection string
in appsettings.json

![[Pasted image 20221223050054.png]]
- data source: server address
- Initial catalog: selects database
	- `Initial Catalog=myNewDB;`
	- this'll create new db if it does not exist.
- Integrated Security-True; -> using the local account as login for a db
	- but in production, it does not work unless you have a Active directory setup
		- in this case we might have to use username/password

We cant Add-migration without tools Package, we'll get this error - ![[Pasted image 20221227055158.png]]


![[Pasted image 20221223050922.png]]
add this ==Tools== in ==web app layer.==

In package manager console, select
`Add-Migration InitialDBCreation` for initial.

This command will fail if you select web app in package manager console.
So, select data access layer.

```cmd
PM> Add-Migration InitialDBCreation
Build started.
Build succeeded.
TO undo this action, use Remove-Migration.
```

Migration script will build out the database.

![[Pasted image 20221223051134.png]]
we can see the migrations inside the migrations folder.




These migration files will have 2 methods.
1. Up
	1. used to do migration
2. Down
	1. things to do before migration

![[Pasted image 20221223051248.png]]
here in this down method, we are seeing the we are simply dropping the tables.
and in UP method, we are recreating it.
This is fine for new tables/databases.
but it can really mess up existing ones, so make sure you go through the scoffolded FIles to see what they are doing exactly.
>Code might be given to you by microsoft, but its your DB at stake, so be careful

we can add as many migrations we want.
lets say I modified one of the models after initial migration. So, then I should add another migration.

## context...Snapshot will have final code that is needed to update the database(this depends on all migrations we've done)
![[Pasted image 20221223052415.png]]

## nvarchar(max)
![[Pasted image 20221223052314.png]]
nvarchar is 2bytes per character, stores unicode
varchar is 1 bytes per character .

nvarchar() can have 1 to 4000 chars
if its more than 4000, we'll use `max`

but sql server has an limit on how much data is stored inside a row.
that is 8060 bytes.
if our data exceeds this limit, sql server will store data in disc.
since it is stored somewhere else, we might end up will all data access issues(like delay, non accessibility etc)

Indexes vs nvarchar(max)
![[Pasted image 20221223052946.png]]
we can make max values indexes,
because non custured indexes have limit of 1700 bytes.


`Update-Database` will update the database

Now we have a database, but not optimized one.

How can we optimize the things we discussed above?
![[Pasted image 20221223053724.png]]
Add Annotations to model properties.
`using System. ComponentMode1. DataAnnotations;`

now, how can we avoid using nvarchar if our db is planned to store only ASCII values?
![[Pasted image 20221223054009.png]]
![[Pasted image 20221223054037.png]]
![[Pasted image 20221223054253.png]]
with our new changes, if we run `add migration`. we get a warning saying this might result in loss of data.

its because, we decreased the size of char, the data will be trunkated if its long.

`Down` method will roll back the schema.
Note that it does not rollback the data.
![[Pasted image 20221226112704.png]]



Then we can `Update-Database `
we can inject the dbcontext using the constructor of class file and use it inside other methods.

we can Initialized some data with a json
![[Pasted image 20221226113230.png]]

![[Pasted image 20221226145345.png]]
we can edit this index.cs file to define what happens during a get request.
![[Pasted image 20221226145603.png]]

here we are trying to see if record count is empty on the db, if yes.
we can insert out dummy value.

![[Pasted image 20221226145614.png]]
we can use event profiler to see all events perfomed on the db.
![[Pasted image 20221226145647.png]]

==Its very important to learn event profiler to see what EF is doing==
we can filter the event profiler to display few things that are coming only from our EF core.
![[Pasted image 20221226150153.png]]
we can see EF executing queries.

for insertion, we could see the EF has done some Batch insert.

Note:
`sp_executesql` is very dangerous command
![[Pasted image 20221226150301.png]]
but since EF knows whats it is doing, this is relatively safer.
But this sp should not be given access to everyone.
```sql
EXEC sp_executesql N'select * from AbpEntityChanges'
```

![[Pasted image 20221226152143.png]]


![[Pasted image 20221226185539.png]]
Also, the sequence of actions we do on the EF query can impact the performance
`.where(x.ApprovedAge(x.Age))`
this cannot be converted to sql query by EF.
so, all commands before it will be converted to SQL, and data is retrieved to do that further processing on the Application end.
This effects the application performance.
So, its better to write inline conditons for where clauses.

Also, the `.ToList()` is done on C# end, so if we have that at the initial stages of EF query. It impacts performance.

SQL servers are designed and optimized to search and find. So, its our job to utilize them properly by sending right commands which does not add extra load on network/application because of redundant data.

# Advantages of EF
1. faster development speed
2. you dont have to know SQL


Dapper is far better according to him.

[[sample queries]]

