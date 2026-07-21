
3 Parameter passing methods - 
- call by value
- call by address
- call by referance



![[Pasted image 20210915095644.png]]
--> pass by value using pass by values
we can see that pass by values is not swapping values in our case.

![[Pasted image 20210915100026.png]]
--> passing by address![[Pasted image 20210915100843.png]]
--> uses seperate memory for pointer variables and temp variable
[[Pointers]]


![[Pasted image 20210915100240.png]]
--> call by referance
just put `&` in function declaration. [[Reference in C++]]

![[Pasted image 20210915100536.png]]

Note that it is not adviceable to use Call by referance.
Because, it is rule that other functions should not be able to share the memory.
so, **machine level code will be made monolithic by the compiler so that the memory can be shared/same for main and called function**.

![[Pasted image 20210917091103.png]]
--> we can mix parameter passing types and it still works.
