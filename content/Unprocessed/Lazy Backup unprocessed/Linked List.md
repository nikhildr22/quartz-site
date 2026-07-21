# why we need dynamic ds linked list
## problem with arrays
1. its of fixed length


## difference bertween array and linked list
| array               | Linked List              |
| ------------------- | ------------------------ |
| memory is contigous | memory is not contiguous |
|                     |                          |
|                     |                          |

# About Linked List

![[Pasted image 20220815143333.png]]

LL is a connection of nodes which contain data and link to next node.

first Node is Head node.

LL is created in heap.

we need two things to define a node.
1. Data
2. Pointer to next node

![[Pasted image 20220815143556.png]]
This kind of structure is called as self referencing structure, as it has an member of same struct type.

size of this node is 4 bytes.
2 bytes of int and 2 bytes for a pointer.

![[Pasted image 20220815143955.png]]

# more about LL
q=p --> q will point to the same node

q=p->next
q will be pointing to next node of p

p=p->next
p will be pointed to next node of p.
here we just moved p to the next node.

## to check if pointer is not pointing anywhere
![[Pasted image 20220815144510.png]]
if its not pointing anywhere, the value will be null or 0.

![[Pasted image 20220815144633.png]]
to check is P is Pointing to a node.


## To check if P is a last node
![[Pasted image 20220815144817.png]]

# Display a Linked list
## how to traverse a LL
![[Pasted image 20220815145104.png]]
as we traverse, we can perform all other operations we were doing on the array on this linked List.

![[Pasted image 20220815145221.png]]

# Diplay LL recursively
traversing recurively

![[Pasted image 20220815145651.png]]
![[Pasted image 20220815145921.png]]

time is o(n)

stack size is n+1, where n is number of nodes.
![[Pasted image 20220815150122.png]]
--> this will print in reverse order.

# Counting nodes in LL
traverse until you get last node, increment counter when you find a new node.

![[Pasted image 20220815150802.png]]
time is n and space is constant.

## recursive method
![[Pasted image 20220815150857.png]]

time and space is o(n)

![[Pasted image 20220815151048.png]]
this is also right approach.

# Sum of all elements in LL
traverse through LL and add values.

we can use while loop, and also recursion.
![[Pasted image 20220815151228.png]]

![[Pasted image 20220815151322.png]]

# Max element in a LL
we need some smallest value, we'll take 16 bit smallest integer.

![[Pasted image 20220815151646.png]]
recursive function:
![[Pasted image 20220815151736.png]]
![[Pasted image 20220815151837.png]]
--> this is easy to read as we have used a ternary operator.

# Searching in a Linked List
1. Linear 
2. Binary search

Binary search is not suitable.

![[Pasted image 20220815152116.png]]

recursive approach:
![[Pasted image 20220815152204.png]]

# Improving searching in LL
we can improve the linear search with 2 methods
1. Transposition
2. Move to head

transposition is swapping with previous value.
in LL we avoid movement of nodes, thus we'll also avoid transposition.

So move to head will be ideal for LL searching.

we need two pointers while swapping nth node with first node.

because while swapping we need to modify the next pointer value of the previous node as well.

q and p will be pointers.
initially q will be pointing to null
and p will be pointing to first node.
as we traverse to 2nd node, we'll  make the q follow p.

when the match is found, we'll use q pointer to change the next address of previous position.

Instead of swapping, we'll change the next pointers to make the nth node as first node.

![[Pasted image 20220815154348.png]]

# Inserting in a LL
we need to indices to know where to insert.
2 cases:
1. Inserting before first node
2. Inserting after given Position

## inserting before first node

create a new node
add data, make it point on the older first node
point the first to new first.
4 steps:

![[Pasted image 20220815154752.png]]

## Inserting after a position
create a new node
initialize the data
point new node to next node, and the previous node's next address should be pointed to this new node.

To do this operation, we need to know the addresses of previous and next nodes.
and we dont know those.

to get the pointer there, we need to start from the first and move it till it reaches the node we desire.

take pointer p on first node,
move p till reaches (n-1) times.
![[Pasted image 20220815155356.png]]

![[Pasted image 20220815155535.png]]

time taken is o(n), the time is due to moving to that particular position.
for worst case its n
for best case its 1. inserting in first position.

## common code to insert before/after a given position
![[Pasted image 20220815160040.png]]

# creating LL using insert
![[Pasted image 20220815160333.png]]

# creating a LL by inserting at last
in the previous method we had to traverse every time when we were inserting at a particular position.

Here we dont have to traverse every time,  just find out the last node and keep a pointer to track the last node.

whenever inserting use last pointer to change the address off next to point to this new node and new node will be pointing to null as next address.

![[Pasted image 20220816093502.png]]

# insert new element in a sorted LL
find a node greater than new element.
when found, insert new element behind the found node.

![[Pasted image 20220816093742.png]]

![[Pasted image 20220816093829.png]]

min time = o(1)
max time = o(n)

# deleting from LL
## deleting first node
move the first node to next position.
deallocate the memory from first node.
![[Pasted image 20220816094110.png]]

![[Pasted image 20220816094151.png]]

we can also keep the data before deleting if its required.

## deleting at a particular position
we'll take 2 extra pointers q and p.
move them one behind one another until p is pointing to required node.

![[Pasted image 20220816094401.png]]
## deleting at any position
![[Pasted image 20220816094542.png]]


## check if LL is sorted
traverse the LL, compare 2 consecutive elements.
or
take one more variable with smallest posible value, compare whole list with low value.
if greater, replace the temp variable value. continue traversal
if the found element is small, the LL is not sorted.

![[Pasted image 20220816094907.png]]


# removing duplicates from sorted LL
![[Pasted image 20220816095329.png]]

# reversing a LL
2 methods:
1. reversing the elements
2. reversing the Links

## reversing the element
use extra array to copy all elements of LL.
then just copy back in reverse order
![[Pasted image 20220816095719.png]]
requires extra space.
requires o(n) time

# reversing a LL using Sliding Pointers/ reversing Links
previous we had q and p, those were tailing pointers as one pointer was following another.

Here we are using 3 pointers and they move together, hence the name sliding pointers.

wow, in one traversal we reversed the LL
![[Pasted image 20220816100221.png]]
at the end, we need to point the first node to q.
![[Pasted image 20220816101302.png]]

This is preferred method rather than movement of data.
because in this example we just had integer values, but if the the data was some complex object data, moving around data would be intensive process, thus reversing the links is more preferred method.

# Recursion for reversing the LL
while returing, we can reverse the Links.
we need two pointers
![[Pasted image 20220816101645.png]]

# concatenating 2 LL
reach the end of 1st LL, then point it to first position of 2nd LL.

![[Pasted image 20220816101907.png]]

time is o(n)

# Merging LL
## merging sorted LLs
we need 4 pointers, first second third last.
first, second --> pointers for original LLs
third, last --> pointers on the final merged LL

1. compare element of first and second
2. if first is smaller
	1. bring third and last on first
	2. move first to next node
	3. make  third and last next address as Null
	4. Last's next should point on second
	5. make last point to second
	6. move second to next node
	7. make last's next as null
3. if second is smaller 
	1. bring third and last on second
	2. move second to next node
	3. make third and last next address as Null
	4. Last's next should point to first
	5. move the first to next node
	6. make last's next as null

![[Pasted image 20220816103444.png]]
This is initial mandatory step

Then loop through the LL and
![[Pasted image 20220816102510.png]]

time is o(m+n)


# Check for Loop in LL
![[Pasted image 20220816103913.png]]

if we are able to find null at the end, there's no loop.

another method is by taking 2 pointers.
he gave a beautiful example of 2 cars, one with faster speed and one with less faster speed.

one pointer moves faster and another at normal speed.

if one of them reaches null, there's  no loop.
if both of them meet at some point, there's loop.

![[Pasted image 20220816104441.png]]
last if block can be replaced with a ternary operatory
![[Pasted image 20220816104521.png]]


# c++  LL
![[84.+LinkedList+CPP.pdf]]

## define a node class
![[Pasted image 20220816105928.png]]

## define LL class
![[Pasted image 20220816110052.png]]

## methods
![[Pasted image 20220816111110.png]]
Initialize LL with a list


# Circular LL
1. last node is pointing to first
2. Links are circularly connected
3. can traverse the list in circular

This is singly linked circular LL

2 ways of representing LL:![[Pasted image 20220816111508.png]]

first one is widely used.
if there are only one element in LL:
![[Pasted image 20220816111947.png]]


for naming conventions, since it is circular in nature, we'll not use `first` and `last` as naming, we'll use `head` to represent the `first` node

Note that a circular LL cannot have a null, even if its empty, unlike Linear LL, it'll point to itself
![[Pasted image 20220816111848.png]]

# Display A circular LL
Traverse until you come back to the `head` node.

we'll use **do while** loop
![[Pasted image 20220816112210.png]]

## recursive display function
![[Pasted image 20220816112522.png]]
note that we are using **static variable**


# Inserting in a Circular LL

## inserting before head or after last node
add new node and point its next to head,
now traverse from head to the end of list,
the last node's next will be modified to point to the new node instead of head.

![[Pasted image 20220816114402.png]]


## inserting at any position
same logic as inserting in a Linear LL
![[Pasted image 20220816114104.png]]

## general function to insert
![[Pasted image 20220816114543.png]]


# deleting node in circular LL
## deleting head node
![[Pasted image 20220816114933.png]]
## deleting node at particular position
same as deleting from Linear LL
![[Pasted image 20220816114731.png]]

## general function for deletion
![[Pasted image 20220816115006.png]]


# Doubly Linked List
![[Pasted image 20220816115107.png]]
every node will have pointer to next and previous node.
![[Pasted image 20220816115151.png]]

![[Pasted image 20220816115211.png]]

the benifit of doubly LL is that we can traverse in both directions.


# insert node in a doubly LL

## inserting before first node
create new node
make next point to first node
make the prev of first node point to new node
make this new node a first node
![[Pasted image 20220816115940.png]]
![[Pasted image 20220816115911.png]]

## inserting at a particular position
this requires 4 modifications
![[Pasted image 20220816120050.png]]

![[Pasted image 20220816120138.png]]


# Deleting a node from Doubly LL
## deleting first node

![[Pasted image 20220816120444.png]]

## deleting at given position
![[Pasted image 20220816120637.png]]


# Traversal, Display and reverse Doubly LL
for traversal, its same logic as single linked linear LL.

![[Pasted image 20220816120827.png]]

## reversing a doubly LL
![[Pasted image 20220816121100.png]]
Scan through the nodes and swap the pointers

![[Pasted image 20220816121026.png]]

# Circular Doubly LL
![[Pasted image 20220816121313.png]]
same logic as singly linked circular LL for traversal.
we use `do while` loop

Inserting logic is same as Linear Doubly Linked List

#rewatch 

# Comparison of LLs
#rewatch 


# Comparison of Array with LL
![[Pasted image 20220816153935.png]]

Insertion Sort and Merge sort are more suitable for Linked Lists.


# finding the middle of the LL
1. method 1:
	1. find the legth og LL
	2. traverse the LL until you reach `n/2` of LL
3. Method 2:
	1. take two pointers p and q
	2. p moves 2 nodes at a time and q moves 1 node at a time
	3. stop q when p is null
	4. ![[Pasted image 20220816162910.png]]
4. Method 3:
	1. use stack to store all elements of LL
	2. pop until you get middle element


# Finding Intersection of two LL
we have to traverse backwards, for this we'll use stack

![[Pasted image 20220816163422.png]]

the point where the stack values start differring, we'd have enountered the intersection point.

![[Pasted image 20220816163550.png]]
