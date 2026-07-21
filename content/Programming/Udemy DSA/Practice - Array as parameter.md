>Note:
 >we cannot call arrays as referance, only we can call by address.


![[Pasted image 20210917092231.png]]
![[Pasted image 20210917092237.png]]

we can notice the size is different because one is pointer and one is actual array.

![[Pasted image 20210917092400.png]]
--> this'll not work, because --> **foreach loop does not work on pointers.**
but it works on normal array in the same scope.

![[Pasted image 20210917092507.png]]
--> so we need to use for loop,
and we can also notice tat we need to size of array also as parameter, or else the function does not know whats the size of the array.

![[Pasted image 20210917092610.png]]
--> this also works.

![[Pasted image 20210917092811.png]]
![[Pasted image 20210917092846.png]]

--> creating array in a function and returning it.
Note that we can use c++ `new` syntax instead of `malloc`