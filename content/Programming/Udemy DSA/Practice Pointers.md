Note:
initializing a pointer with an arrray:

![[Pasted image 20210914095700.png]]
pointer acts just like a name of an array.

and while initializing we dont need to use `&` sign here for array.

Using heap memory:

p is in stack.
array is inside heap.
![[Pasted image 20210914095858.png]]
--> C
![[Pasted image 20210914095909.png]]
--> C++

after using the memory we need to decallocate the momory.
![[Pasted image 20210914100028.png]]
--> Deallocating the heap memory in C++ `delete [] p;`
![[Pasted image 20210914100021.png]]
--> deallocation in C `free(p);`

dynamically allocation memory should always be deallocated after usage.

for small programs, it does not affect any performance.

But for large programs, we need to take care of all these memory management.

![[Pasted image 20210914100324.png]]
-->![[Pasted image 20210914100336.png]]
size of every pointer same irrespective of type of pointers.