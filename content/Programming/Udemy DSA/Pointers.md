Pointer is a address variable.

its using to store the address of a data.

these are used to indirectly access the data of the variable

 ![[Pasted image 20210914093000.png]]
 as we know main memory is divided into 3 sections.
 - heap
 - stack
 - code

code section can directly access the data in code section and stack section.
But it cannot directly access the data in the Heap memory.

>So, thats why need pointers for this operation.

for accessing external resources -> the program needs pointers.

why we need pointers?
![[Pasted image 20210914093228.png]]
resources like keyboard, internet etc.


How to declare initialise and how to use it?

```c

int a=10; //data variable 
 
int *p; //address variable

p = &a; //p stores address of a
printf("%d", p ) //prints the address
printf("%d", *p ) //deferencing a pointer

```

getting the data using pointer is called **dereferencing**

>Note:
>- while declaring use *
>- while initializing use *
>- While dereferencing use *

in this example we are not accessing a heap memory.

example for using heap memory:

to use heap memory we need to use **malloc** in C language.

we must use `stdlib.h`

![[Pasted image 20210914094052.png]]
since the size of the variable is dependant on the compiler, we are making it dynamic while allocating a memory for a pointer using malloc.

>this is the syntax for allocating memory to the pointer and remember that
>**malloc** returns a void pointer, we have to type cast it to a int pointer `(int *)malloc(S*sizeof(int));`


in C++ its easy to allocate memory by just using `new`  keyword.
`p = new int[5]; //code in c++`



[[Practice Pointers]]