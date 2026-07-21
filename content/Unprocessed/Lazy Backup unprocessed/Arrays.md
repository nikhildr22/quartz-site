
# Intro to arrays
![[Pasted image 20220718093437.png]]

scalar variable: single valued variable.

Vector variable: multiple valued variables.

Arrays are vector variables.

memory allocation for array is contigous.

Elements can be accessed using name and index of the array.

# Declarations of array
when declared the values inside the array will be garbage values.

variaous ways of initialization of an array:

![[Pasted image 20220718093947.png]]

- [x] when will be array created? runtime or compile time? 
==memory allocated during runtime, but memory is calculated during compile time==

Traversing array: using a loop.

Various ways of accessing elements of an array:

![[Pasted image 20220718094216.png]]

# Static vs Dynamic arrays
size of array is static and size of an array is dynamic.

size of the memory required will be calculated during compile time.
memory will be allocated during the runtime.

the size of array should be constant value in C language.

But in C++, variable sized arrays can be declared.
`int a[n]` -> this is valid

## How to create array in heap.
we need a pointer.

![[Pasted image 20220718094855.png]]
we've to use malloc in c language.
in c++ new keyword can be used to create array in heap.

![[Pasted image 20220718095020.png]]

make sure you free the heap memory done using.
[[Static vs dynamic memory allocation]]
Now we can use the pointer as name of an array, we can access the elements of the array.

>array inside the stack cant be resized.
>But if the array is inside the heap, we can increase/decrease the size of the array.

# Increase the size of the array.
![[Pasted image 20220718095631.png]]
we've to create a new array in heap and copy everything there.
make sure you delele unused p.
![[Pasted image 20220718095740.png]]
deallocated p.
point p to q
make q point to null.

# 2D arrays
3 methods of creating 2D array:
1. with name and dimentions `int A[m][n]`
	1. initilization: `A[][]={{}.{}}`
2. Using Pointers `int *A[3]`
	1. ![[Pasted image 20220718100545.png]]
3. double Pointer `int **A`
	1. `A= new int *[3]`
	2. ![[Pasted image 20220718100722.png]]

these above 3 are
1. completely in the stack
2. partial in the stack and partial in the heap
3. everything in heap
![[Pasted image 20220718101611.png]]


## How to access elements of 2D arrays:
using nested for loops.


## Array Representation by Compiler
formula used by compiler to find any address of the array.
Only base address is required to remember by the compiler.
![[Pasted image 20220731043142.png]]

### 1 indexed arrays
![[Pasted image 20220731043308.png]]

in c/c++ its strictly 0 indexed array.

> if we compare the formula used to compute the location of an array element, 1 indexed array has an extra operation(substraction), thus it is slower compared to 0 indexed arrays.

## Row Major formula for 2D arrays
Note that even though we represent a matrix as 2D on paper, but inside computers while allocating memory, its a linear memory allocation.

2 representations:
1. Row Major mapping
2. Column mapping

### Row Major mapping
elements are stored row by row.
![[Pasted image 20220731043751.png]]
![[Pasted image 20220731044032.png]]

### COlumn Major mapping
![[Pasted image 20220731044235.png]]
![[Pasted image 20220731044916.png]]

we can use these formulas if we are designing our own compiler.

## Formula for nD arrays
for 4D array:
![[Pasted image 20220731045231.png]]

for nD array:
![[Pasted image 20220731045425.png]]

Analysis of row major formula:
![[Pasted image 20220731045731.png]]

we got order of n square. and this is too much of multiplications.

we'll user Horners rule to reduce number of multiplications:
![[Pasted image 20220731045915.png]]
## Formulas for 3D arrays
![[Pasted image 20220731050148.png]]
we might get confused with the terms rows and columns for 3D matrix, as its 3D.
thus dont call them as rows and columns, just write the formula.

