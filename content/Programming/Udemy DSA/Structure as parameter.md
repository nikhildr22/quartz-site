Pass by value:

seperate object gets created and struct values get copied into thet new object inside the function.

![[Pasted image 20210917093421.png]]

any modification to struct inside the function will not reflect in the actual parameter.

Call by reference:
![[Pasted image 20210917093556.png]]
--> this'll modify actual parameter.

Call by Address:

 ![[Pasted image 20210917093843.png]]
 we need to pass the address.
 in formal parameter should be a struct pointer.
 
 ![[Pasted image 20210917094017.png]]
 --> consider having array as data member of struct.
 
 >Note that we cannot pass array as call by value.
 >But struct can be called by values.
 >so, it works to pass struct as value even though it has an array as data member.

but it includes some data copying process in the backend and it could be inefficient.
**But it works**