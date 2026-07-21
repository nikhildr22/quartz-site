LIFO  - last in first out 

![[Pasted image 20220816164030.png]]

we can implement stack using and Array and Linked List

# stack using array
we need 3 things array, size, and pointer to the top.
![[Pasted image 20220816164602.png]]

![[Pasted image 20220816164547.png]]

## check if stack is empty/full
![[Pasted image 20220816164659.png]]

# operations on Stack
## push
1. increment top
2. insert value at `stack[top]`
3. before insertion check if stack is full

![[Pasted image 20220817052856.png]]

## Pop
1. take out the value at top
2. decrement top
3. check if `top==-1` before you delete

![[Pasted image 20220817053112.png]]
This'll return -1 if the stack is empty.

## peek
finding element at given position

its just like array indices, but in reverse order and depends on the top of the stack
![[Pasted image 20220817053253.png]]

therefore, the equation to get the index from position will be:
`index = top - pos + 1`
if this index is less than 0, its an invalid position.

![[Pasted image 20220817053513.png]]

## stackTop
![[Pasted image 20220817053552.png]]

## stackIsEmpty
![[Pasted image 20220817053619.png]]

## stackIsFull
![[Pasted image 20220817053650.png]]

# coding stack using array
[[stack using cpp array]]

# Stack using LL
in LL we know the insertion takes different time depending on where were inserting
![[Pasted image 20220817054030.png]]
since insertion from first node takes constant time, we'll insert in this end.

## to check if stack is empty
![[Pasted image 20220817054321.png]]

## to check if stack is full
![[Pasted image 20220817054338.png]]
since LL size is not limited like arrays, stack can have unlimited size, but when we are unable to create  a new node, that time we can consider as stack is full.

# Stack operation using LL
## Push
1.  create a node
2. if node not created, then stack is full
3. else
	4. add data to newly created node
	5. point the new node's next to previous top node
	6. assign top pointer to this new node

![[Pasted image 20220817055414.png]]

## Pop
1. check is top is empty
2. if not delete the top node
3. move the top to next node
4. free deleted memory
![[Pasted image 20220817055535.png]]


## Peek operation
1. traverse and return value
2. if the value there is null, return -1

![[Pasted image 20220817055702.png]]



## stackTop
![[Pasted image 20220817055808.png]]

## isEmpty
![[Pasted image 20220817055820.png]]
## isFull
![[Pasted image 20220817055829.png]]




# stack using LL
[[stack using cpp Linked List]]

# Parenthesis matching using stack
1. traverse through the equation
2. if opening bracket, push into stack
3. if closing bracket, pop from stack
4. at the end if the stack is not empty, the stack is imbalanced.

![[Pasted image 20220817060504.png]]
here we need s stack of characters:
![[Pasted image 20220817061626.png]]


Intially the function would look like this:
![[Pasted image 20220817061747.png]]

iterate through the equation:
![[Pasted image 20220817062011.png]]
[[225.BalancedParenthesisUsingLLBasedStackC++.txt]]

# if there are multiple types of brackets in an equation
[[226.ExtendedBalancedParenthesisUsingSTLStack&MapC++ (1).txt]]
![[Pasted image 20220817062710.png]]

some extra logic




# Infix to Postfix conversion
![[Pasted image 20220817062841.png]]

to solve any expression, we need BODMAS rule.
but how can we make computer know that?
![[Pasted image 20220817063137.png]]
consider this equation.

if we need to find the answer in one go, we can't get the right answer using infix form.

But by using Postfix form we can get the right answer.

This is a postfix equation:
![[Pasted image 20220817063343.png]]

How to write PostFix:
This is a precedence table:
![[Pasted image 20220817063420.png]]

>for best practices, we need to feed the computer with fully parenthesized equation.
>If the equation is not fully parenthesized, the compiler will parenthesize internally using the rules of precedence.

Postfix is widely used.

## writing prefix
![[Pasted image 20220817064051.png]]

## writing postfix
![[Pasted image 20220817064119.png]]

## ANother example
![[Pasted image 20220817064259.png]]

# Associativity and Unary operators
![[Pasted image 20220817080048.png]]

if precedence is equal, we'll look for associativity. from `R --> L` or `L --> R`

![[Pasted image 20220817080308.png]]



Postfix is dependant on parenthesization and parenthesization is dependent on associativity.

![[Pasted image 20220817080555.png]]

## unary operators
#todo/paused 