
>Arrays can only be passed by address in c++



![[Pasted image 20210917091403.png]]

here `A[]` --> is a array pointer exclusively.

if we use `int *A` --> this can be interger pointer and as well as array pointer.

Array modified inside a function will also modify the original array --> because it was passed by address.

How can you return an Array?

 ![[Pasted image 20210917091803.png]]
 
 ![[Pasted image 20210917091833.png]]
 --> we can also use `*` in function declaration instead of `[]`
 >==NOTE:==
 >USe `*` not `[]` because some compilers dont allow `[]`
 
 
 
 
[[ Practice - Array as parameter]]
 
 