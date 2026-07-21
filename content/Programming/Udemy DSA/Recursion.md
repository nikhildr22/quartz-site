[[How Recursion Works]]

---

[[Generalizing Recursive function]]

---


[[How recursion uses stack]]

---

[[Time complexity of recursion]]

----



---


[[Static variables in recursive function]]

---

 [[Types of recursion]]
 ---
 
 [[Tail recursion]]

---


[[Head recursion]]

---

[[Tree recursion]]

---

[[Indirect recursion]]
---

[[Nested Recursion]]

---

[[sum of first n natural numbers using recursion]]


---


[[Factorial using recursion]]

---
[[Power or exponent using recursion]]


---

# Taylor series using recursion
![[Pasted image 20220309100138.png]]

n number of terms determine the precision of the output.

we have 3 recursions here, but we need just one final output to be returned.
we can notice that addition, multiplication and power is done during returning time. aka its not a tail recursion.

![[Pasted image 20220712091645.png]]

lets consider p and f as static variables to store power in numerator and factorial in denonimator and they'll be initialized to 1.

![[Pasted image 20220712091915.png]]

![[Pasted image 20220712092121.png]]


e(x,n)-> x= power, n= precision while using the series formula

---



# Taylor series using Horner's rule
we can further reduce the number of multiplications.

#rewatch  


---
# Fibonacci series 
![[Pasted image 20220404092021.png]]

initially there has to be 2 terms.
![[Pasted image 20220404092219.png]]
![[Pasted image 20220404092305.png]]
![[Pasted image 20220404092423.png]]
--> iterative version
O(n) time complexity.


![[Pasted image 20220404092705.png]]
--> 2 power n order,
this is very large compared to iterative version.
This is because of ==excessive recursion==
i.e., same calculation is done at different times during different fucntion calls,
example: fib(3) fib(2) are called multiple times where the result could have been used.

we'll use static array or global variable to store the knows values.
![[Pasted image 20220404093118.png]]
--> o(n) 
this is called ==memoization==
- [ ] study memoization https://www.geeksforgeeks.org/what-is-memoization-a-complete-tutorial/

![[Pasted image 20220404093230.png]]



---

# Combination formula (Selection of subset)
if the set of objects is given, in how many ways we can select the subset.

nCr
![[Pasted image 20220404093720.png]]
![[Pasted image 20220404093839.png]]
![[Pasted image 20220404093953.png]]
--> Pascal's triangle
![[Pasted image 20220404094043.png]]
for extreme values n=0 and n=r, the answer is 1.

- [ ] studying properties of Pascal's triangle


---


# Tower of Hanoi

![[Pasted image 20220713045133.png]]
Discs are kept on A.
All discs should be transferred to C by following the conditions:
- move one disc at a time
- no larger disc should be kept over smaller disc
![[Pasted image 20220713045356.png]]
B is auxillary tower which can be intermediate tower between A and C.

This problem was belived tobe unsolvable problem, but this can be solved with recursion.

## when we have just 1 disc
![[Pasted image 20220713045546.png]]

![[Pasted image 20220713045605.png]]

though we are not using B, we are assuming we used B.
same applies when we increase the number of discs.

## when there are 2 discs
![[Pasted image 20220713045649.png]]

![[Pasted image 20220713045931.png]]
>1. Move from A to B by using C are auxilarry
>2. move from A to C using B
>3. move from B to C using A

==Note:==**though we are not using auxillary tower in all places, we are assuming we used it for the sake of computation and formulas.**


## When we have 3 discs

![[Pasted image 20220713050504.png]]

## for n discs
![[Pasted image 20220713050801.png]]

![[Pasted image 20220713051630.png]]

it is more like in-order tree traversal.

## time complexity of tower of hanoi solution
![[Pasted image 20220713051908.png]]

```cpp
#include <stdio.h>
void TOH(int n,int A,int B,int C) 
{ 
    if(n>0) 
	{
		TOH(n-1,A,C,B);
		printf("(%d,%d)\n",A,C);
		TOH(n-1,B,A,C); 
	}
}
int main() 
{ 
 
 TOH(4,1,2,3);
 return 0;
 
}
```