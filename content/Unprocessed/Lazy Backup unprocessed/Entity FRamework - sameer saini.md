---
alias: []
Status: 
Medium: 
Tags: 
url: https://youtu.be/3NWT9k-6xGg
---
___
# Entity FRamework - sameer saini

![[Pasted image 20221217050409.png]]
![[Pasted image 20221217050426.png]]

we'll use inmemory database
![[Pasted image 20221217050528.png]]

we need a model
![[Pasted image 20221217050555.png]]

we can use a class to talk to a database for us using EF.
that class we call as DbContext
![[Pasted image 20221217050658.png]]

![[Pasted image 20221217051334.png]]

we need to create a class that inherits dbcontext.

then we need to add  a constructor for it which requires options.
we can do that by clicking control+dot on classname.

then we need to add properties, which act as table


![[Pasted image 20221217051540.png]]
we need to inject this new dbcontext

