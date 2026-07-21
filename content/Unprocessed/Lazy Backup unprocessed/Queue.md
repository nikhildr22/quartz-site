FIFO  - First In First Out

Queue has 2 end, `front` and `rear`

![[Pasted image 20220817101618.png]]
queues cab be implemented using Arrays and Linked Lists.

# implement Queue using Array
## using single pointer
![[Pasted image 20220817101810.png]]
we just have one pointer `rear` 
we'll move the rear whenever we want to insert.

whenever we want to delete, we'll delete the element. we've to move all the elements to fill that blank space and also we need to move the rear.

insert = o(1)
delete = o(n)

## using 2 pointers - front and rear

![[Pasted image 20220817102130.png]]

initially queue is empty.
move the rear pointer and insert element.
for deletion, move the front pointer and delete the element.
note that front will stay at a deleted position, whenever we need to deque, we'll move the front to that position and delete the element.

enque = o(1)
deque = o(1)

### empty
when `front==rear`

### full
when `rear==size-1`

## implementation
![[Pasted image 20220817102629.png]]
![[Pasted image 20220817102750.png]]
### enqueue
check if queue is not full
increment rear and insert value
![[Pasted image 20220817102920.png]]

### Dequeue
check if queue is not empty
if not, delete the front element
move front to next position

![[Pasted image 20220817103037.png]]
[[242.QueueUsingArrayC++.txt]]

## Drawbacks of using Array for Queue

![[Pasted image 20220817103332.png]]
in this scenario, even though few positions are empty, the rear end is not empty and this makes queue as full.
so inserting new elements is not possible using our method.

i.e., we cannot re utilize the position of deleted elements.
or every location can be used only once.

![[Pasted image 20220817103532.png]]
in the above situation, even though the queue is completely empty, we cant insert new element because our logic was different.

## solutions for drawbacks
1. resetting Pointers
2. circular queue


# Circular Queue
The idea is that, rear when reaches the end of queue.
and if there are empty positions before front, rear will go behind the front.
![[Pasted image 20220817104057.png]]
For this we'll use `mod` operation

![[Pasted image 20220817104147.png]]

here the array is not circular, but `front` and `rear` pointers move circular.

## enqueue
check if queue is  full
	if next position to `rear` is `front` pointer
	then queue is full

![[Pasted image 20220818101053.png]]
--> in this case, next position to `rear` is `front`
![[Pasted image 20220818100816.png]]

## Dequeue
if not empty, then dequeue
![[Pasted image 20220818101254.png]]


# Queue using Linked List
we'll take two pointers on LL.
`front` and `rear`

if `front==null`, then queue is empty

if `front==rear` then queue has only one element.

as its LL, the size is unlimited..
but we are unable to create a new node, we'll consider that situation as queue is full.


## Enqueue
check if queue is full
if not, set data, and set next pointer as null.

if front was null, this new node is the first node.
so now point front and rear to this new node.

if there were nodes already, 
assign the next value of rear to this new node.
move the rear pointer to this new item.

![[Pasted image 20220818101754.png]]

## dequeue
check if queue is empty
if not delete the front node.
![[Pasted image 20220818102103.png]]


# Double ended queue - DEQUEUE
in this we can use both rear and front pointers for insertion and deletion.
there's no FIFO restriction.

some languages support this DEqueue data structure. ex:java


![[Pasted image 20220818102232.png]]

2 types:
1. input restricted DEQueue
2. Output restricted DEQueue


# Priotity queue
2 methods:
1. Limited set of priorities
2. Element priority

## Limited set of priorities

each element will have its own priority.
for example java supports 10 priorities.

and This logic is widely used in Operating systems.

![[Pasted image 20220818103223.png]]
this example has 3 priorities and 3 is lowest priority and 1 is highest priority.

we'll take 3 priority queues
![[Pasted image 20220818103409.png]]
before inserting, we'll check the priority and then insert.
![[Pasted image 20220818103445.png]]

but while deleting, you've to go by the priority of the queue.
In our case, we've to delete the item from Q1.

## Element priorities
in this method, depending on the value of the element, the priority is decided.
we can set any rules as per our requirements for setting the priority.

lets take a integers as example.
and set rules as, smaller the number, higher the priority and vice versa.

This is Not FIFO.
we can have 2 methods:
1. insert in same order
	1. delete the higher priority element by searching it
	2. after deletion we've to shift the elements
2. insert in increasing order of priority
	1. delete last element of array
	2. while insertion we've to shift other elements



# Implementation of Queue using 2 stacks

push elements in to S1 stack.
then transfer them to S2, if s2 is empty.

start dequeing from S2.

![[Pasted image 20220818104453.png]]
