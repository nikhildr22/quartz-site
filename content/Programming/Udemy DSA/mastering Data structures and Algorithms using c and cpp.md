dont skip time and space complexity.

---
[[Topics covered]]:

[[Memory basics]]





![[Levels of DSA mastery]]


C languages dont have built in data structures.
so here we are concentrating on C.

Why C in this course?
it lacks built in data structures.


course structure:
- basics of c and C++
- sorting and recursion are covered in beginning.


![[Problem solving vs Programming]]

 
 
 >this course is about ds and the algos applied on those ds.
 >since algos is a very vast topic -> refer his youtube channel

---

[[Array Basics]]

---
[[Arrays Practice]]


---



[[Structures]]



---



[[Pointers]]

#paused-revision

---




[[Reference in C++]]



---



---

[[Pointer to a structure]]



---

[[Functions]]






---

[[Parameter passing]] methods

---


[[array as parameter]]

 
 ---


[[Structure as parameter]]


---

[[structures and functions]]:


---

[[Converting C program to C++]]


---

[[Monolithic programming]] Vs [[Modular programming]]




---


[[Practice - Structures and Functions]]



---

[[Object oriented Programming]]



---

[[C++ class and constructor]]

---
 [[Template classes]]
 
 
 ---
 
 # section 4
[[intro to DS]]

[[Static vs dynamic memory allocation]]

---

[[Physical and logical data structures]].


---
[[ADT]]:

---
Time and space complexity

time complexity:

order of n --> o(n)
#rewatch

---

analyzing time and space complexity using code:

time function:
polynimical equation obtained after analizng the time complexity of the code.

![[Pasted image 20210927095325.png]]
![[Pasted image 20210927095353.png]]
![[Pasted image 20210927095423.png]]
![[Pasted image 20210927095656.png]]

---

How recursion works
![[Pasted image 20210928090125.png]]

A function calling itself
![[Pasted image 20210928090259.png]]

base condition --> to terminate the recursion.

![[Pasted image 20210928090400.png]]
--> example

how to trace a recursive function?
it is tracked using a tree.


![[Pasted image 20210928090621.png]]
this is called as tracing tree of recursive function.

Another example:

![[Pasted image 20210928090848.png]]
we can notice that the order of printing was reversed by swapping 2 lines of code in the function.
so, we have to keep track of the function calls in the recursive function.

analogical example:
![[Pasted image 20210928091250.png]]

i.e., recursion has two phases, calling phase , returning phase.

we can compare recursion to a rubber band -> it goes on expanding, but once the condition is met, it comes back.

---

Generalising Recursion
![[Pasted image 20210928091541.png]]

lines before recursive line are executed during the calling time

lines after recursive line (or recursive call), will be executed during returning time.

![[Pasted image 20210928091756.png]]
it can also be called as ascending and descending.

Comparing recursion with loops:
- both are repeating
- but loop only has ascending phase


---
How recursion uses stack?

![[Pasted image 20210928092147.png]]

for this program, it requires n+1 calls.
and since the degree is 1, the order is o(n).


---

how to find the time complexity of recursive function?
how to find using the trace tree:
![[Pasted image 20210928093241.png]]

How to find using Recurrant solutions:


![[Pasted image 20210928093439.png]]
![[Pasted image 20210928093501.png]]

---

Recursion practice

---

Static and Global variables in recursion

example with local variabels:
![[Pasted image 20210928094446.png]]

examples with static variables:

static varibles are created inside a code section and there'll only be a single copy of static variable for entire function.

![[Pasted image 20210928094817.png]]

![[Pasted image 20210928094900.png]]


---

Types of Recursion
![[Pasted image 20210929091324.png]]

1. Tail recursion
![[Pasted image 20210929091352.png]]
if recursive call is the last line in that function, tat is tail recursion.

and everything other operation performed during calling time.
and during  returning time, no operation is performed.

Tail recursion vs Loop:

![[Pasted image 20210929091554.png]]

time is o(n) for both of above.

![[Pasted image 20210929091653.png]]
space complecity is better for loop. therefore if there's a scenario, we can use loop instead of tail recursion.

tail recursion -> created n stacks for n calls.
but forloop requires only one stack space.

---
Head Recursion
![[Pasted image 20210929091847.png]]

all processing is done at returning time.

head recursion vs Loop:

![[Pasted image 20210929092132.png]]
we can notice that head recurion cannot be converted to loop as it is. But its not impossible.

---
Tree recursion

Linear recursion:
function calling itself only once.
![[Pasted image 20210929092309.png]]

Tree recursion:
![[Pasted image 20210929092358.png]]

tracing the  tree recursion:



![[Pasted image 20210929092939.png]]


![[Pasted image 20210929093024.png]]

time complexity:
![[Pasted image 20210929093251.png]]
 it was calculated by counting how many function calls were made at each level of tree.
 
 Space complexity:
 its depends on the maximum stack height.
 but as we saw, same stack will be allocated and deallocated . (used again and again).
 
 Thus, space complexity is height of the tree.
 here it was 4 for n=3
 therefore -> n+1 --> o(n) as space complexity.
 
 ---
 
 Indirect recursion
 
 more than one function calling one another --> forming a cyclic call.
 
 ![[Pasted image 20211004090902.png]]
 
 example:
 ![[Pasted image 20211004091114.png]]
 
 
 ---
 Nested recursion:
 
  ---
  example - sum of First n natural numbers.
  
  ![[Pasted image 20211018093607.png]]
  
  ![[Pasted image 20211018093656.png]]
  
  but there's a formula, we can use that also.
  
  ![[Pasted image 20211018094031.png]]
  ![[Pasted image 20211018094058.png]]
  
  we can see that mathemaical representations can be easily converted into recursion, but they use lot of memory(stack).
  
  ---
  factorial using recursion.
  ![[Pasted image 20211018094659.png]]
  ![[Pasted image 20211018094710.png]]
  ![[Pasted image 20211018094857.png]]
  
  ---
  power using recursion
  ![[Pasted image 20211018100225.png]]
  ![[Pasted image 20211018100319.png]]
  ![[Pasted image 20211018100424.png]]
  ![[Pasted image 20211018100550.png]]
  how to reduce the number of multiplications in the above example?
  ![[Pasted image 20211018101005.png]]
  --> code
  ![[Pasted image 20211018100923.png]]
 
 
 
 









 
 
 
 















