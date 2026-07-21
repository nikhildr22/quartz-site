collection of similar data items under one name.

this is for user defined data types.

in OOPs we use classes and since we are using C here, we use struct.

Example:
Rectangle - 

```c
struct Rectangle
{
	int length;
	int breadth;
}
```

this struct is taking will take 4 bytes of memory.

```c
int main()
{
	struct Rectangle r;
	struct Rectangle r = {10.5};
}
```

struct memory is allocated in stack memory.

struct variables can be accessed using a dot operator.

r.length , r.breadth

we can read/write/update using dot operator.
![[Pasted image 20210914091037.png]]
another example:
Complex number - 

a+ib
```c
struct Complex
{
	int real;
	int img;
}
```

memory consumption:
![[Pasted image 20210914091252.png]]
==its the size consumed by all its members==.

We can also create array of struct (it is just like any other data type)

