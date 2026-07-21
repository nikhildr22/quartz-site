# terminology of Tress

Tree is a collection of nodes and edges.

if there are n nodes, there are n-1 edges.

there'll be a root node.

all nodes below root are subtree/subset.

a node is a parent to very next nodes.

siblings are children of same parent.

decendants: all nodes that can be reached from a particular node.

Ancestors: all nodes from that node to root node.

degree of a node: number of children.

internal/external nodes: nodes with degree 0 are external nodes/ leaf nodes/ terminal nodes.

nodes with degree greater than 0 are called internal nodes.


Level: level of the node from the root. here we'll count the nodes.
at first level there was one node, thus it starts from 1.

height of tree: we'll count the edges. at first position we had 0 edges, thus the height starts from 0.

Note that level starts from 1 and height starts from 0
![[Pasted image 20220818105223.png]]


Forest:
COllection of trees is called forest.


# Binary tree
The degree of tree is 2.

![[Pasted image 20220818105435.png]]

it cant have not more than 2 childrens.
children will be named left child and right child.

children can be 0 or 1 or 2. not more than 2.


![[Pasted image 20220818105650.png]]
left and right skewed binary tree.

![[Pasted image 20220818105720.png]]
--> this is not a binary tree.

# Number of Binary trees for given number of nodes

two types of nodes:
1. unlabled nodes
2. labled nodes


## unlabled nodes
![[Pasted image 20220818110527.png]]
![[Pasted image 20220818110556.png]]
catalan number is used to find out the number of possible number of binary trees for given number of nodes.

### How many binary trees possible with maximum height
![[Pasted image 20220818110832.png]]

### Another formula for catalon number
![[Pasted image 20220818111104.png]]
we obtained this formula by seeing the pattern when we jotted down the values of first formula on the table.
![[Pasted image 20220818111214.png]]
![[Pasted image 20220818111255.png]]

this new formula is recursive formula.


## Labled nodes
![[Pasted image 20220818111440.png]]
if the nodes are labled, each tree can be represented in n! ways where n is number of nodes.
Thus, we should multiply the final value obtained with n!.


# Height vs Nodes
## if height is given
if a height is given, what is the min number of nodes and max number of nodes possible in a tree
![[Pasted image 20220818111653.png]]

min nodes `n = h+1`

for max number of nodes in a binary tree.
we'll use GP series
![[Pasted image 20220818111837.png]]
![[Pasted image 20220818111926.png]]

## if number of nodes are given
![[Pasted image 20220818112337.png]]

![[Pasted image 20220818112426.png]]


# Internal vs External nodes in Binary tree
![[Pasted image 20220818112646.png]]
this formula is always true for Binary tree.


# Strict Binary tree
also called as proper/complete binary tree.

in a strict binary tree, the node can have either 0 children or 2 childre.
a node cant have 1 child.

# Height vs Nodes in Strict Binary trees
max nodes are same as general binary tree.

but min nodes are different here.
![[Pasted image 20220818113052.png]]
![[Pasted image 20220818113138.png]]
![[Pasted image 20220818113227.png]]


# Internal Nodes vs External Nodes in strict Binary trees

![[Pasted image 20220818113332.png]]
this condition is always true in strict Binary trees


# n-ary trees
n is the degree of a tree.

![[Pasted image 20220818113656.png]]

![[Pasted image 20220818113721.png]]

structure of a node in a tree:
![[Pasted image 20220818113745.png]]
this node has a capacity of having 4 children.
and 4 is maximum.

so the degree of a node is pre defined, and we cant determine the degree by looking at the tree.

a 4-ary tree is also a binary and 3-ary tree.

## strict m-ary trees
strictly having either 0 children or m children.

# Analysis of height vs node of strict m-ary trees

![[Pasted image 20220818114248.png]]
![[Pasted image 20220818114339.png]]

## number of internal vs external nodes
![[Pasted image 20220818114517.png]]


# Representation of Binary tree
## Array representation
consider an array starting from 1.

but how do we preserver the position of nodes in a tree?
we'll use indices.
![[Pasted image 20220818114846.png]]
we'll use this formula to find the childrens.

How to find the parent?
![[Pasted image 20220818114944.png]]


## Linked representation
we'll use nodes for representation.
![[Pasted image 20220818115054.png]]
![[Pasted image 20220818115118.png]]

for any shaped binary trees, if there are `n` nodes, there'll by `n+1` null pointers.


for writing algorithms, we'll use this linked representation on Binary tree.


# Full and COmplete Binary tree

if a binary tree of height h having max number of nodes, then this is full binary tree
![[Pasted image 20220818115632.png]]

## Complete Binary tree
if a tree is represented in a array, 
and if there are empty spaces between elements, then its not a complete binary tree
![[Pasted image 20220818115834.png]]

full binary tree is always a complete binary tree.
But not vice versa.

# strict vs Complete Binary tree
if strict is complete,  then complete is almost complete

![[Pasted image 20220818122133.png]]


# Tree traversal
![[Pasted image 20220818122526.png]]
![[Pasted image 20220818122603.png]]
![[Pasted image 20220818122854.png]]

# easy method 1 to find traversal of binary tree

![[Pasted image 20220818123150.png]]
![[Pasted image 20220818123204.png]]
for pre order, draw lines on left side of nodes such that they dont intersect with any other lines.

for post order, draw lines on right side of the nodes such that they dont intersect with any other lines.

for In order, draw lines straight to the bottom.

take the order from Left to Right.


# Easy Method 2
![[Pasted image 20220818124046.png]]
![[Pasted image 20220818124059.png]]

Pre order - draw line on left
In order - draw line on the bottom

Post order - draw line on the right

after you draw line on the node, start traversing the boundary of the tree,
whenever the boundary intersects with a extruding line mark that node as next traversal node.

# Easy method 3 (easiest)

same as second easy method, just dont draw lines, use left and right hands.


# Create a Binary tree using Linked representation
we'll use a queue to track the address and order of nodes.
add first root node in the queue.

whenever we are adding a new node, take out an element from the queue, check if there's left/right childs.
if there are left and right childs.
create nodes and add the address of those children in the queue.

Once we've added children for the root node.
we'll take the next item in the queue.
and repeat the same procedure.

This process goes on until the queue becomes empty.

# Program for creating Binary Tree using Nodes

we need to define node structure.

we need a queue using LL. LL because we dont know the size of queue.

![[Pasted image 20220818125639.png]]

the block in the red should be repeated again for the right child.
[[271.TreeClassUsingArrayQueueC++]]

[[271.TreeClassUsingSTLQueueC++]]




# Pre order traversal
![[Pasted image 20220819061127.png]]
![[Pasted image 20220819061437.png]]

number of activation records created depends on the height of the stack.

number of recursive calls is `2n+1`
n calls for nodes with children, n+1 calls for nodes with no children

# Inorder traversal
![[Pasted image 20220819061851.png]]


number of recursive calls is `2n+1`

number of activation records created depends on the height of the stack.

# post order
DIY

# Iterative functions for tree traversals
## preorder
for converting recursion to loops, we might have to use our own stacks.
![[Pasted image 20220819063944.png]]

## Inorder
![[Pasted image 20220819064200.png]]
its is almost similar to Preorder

## Postorder
![[Pasted image 20220819064230.png]]
this is bit different than last 2.

we need to push the addresses consecutively twice.
thus, there arises a problem to determine which was for `right` and which was for `left`

for we'll convert the address negative integers while pushing for one of the sides.
while popping we can convert them back to actual addresses.

![[Pasted image 20220819064716.png]]

[[276.TreeIterativeOrderTraversalUsingSTLStackC++.md]]

# Level order traversal of Binary tree
we'll use queue to implement iterative Level order traversal.
visit every node, enque left and right child.
then take the next adress in the queue.
continue till the queue becomes empty.


![[Pasted image 20220819065733.png]]

[[278.LevelOrderTraversalC++.md]]



# can we generate tree from traversals?
## for preorder/post/inorder

![[Pasted image 20220819092718.png]]

from a given traversal, we can come up with multiple patterns of trees.

so we cant come up with tree with only pre order is given.

![[Pasted image 20220819092849.png]]
we can come up with these many number of trees.

## if pre and post order traversal is given
more than one trees can be generated.

## preorder+inorder and Postorder+Inorder
this can be done, because inorder starts with root, we can easily come up a tree if we include inorder along with post/pre order.


# Generating trees from traversal
any two traversals are compulsary and one of them must be inorder.

## preorder+inorder
![[Pasted image 20220819093638.png]]
write all elements of inorder in the given order.

take first element from preorder list.
find the position of this inorder array,

the make that as root node.
split the elements on its either side to different arrays.
now do this operation recursively for all other elements in the preorder array.

# height and count of Binary tree

## count the number of nodes
![[Pasted image 20220819094335.png]]
recursively we'll count the node and add them up.

and this is working similar to post order traversal.

==post order is most commonly used on Binary trees for of the traversal==


## to count nodes with degree 2
![[Pasted image 20220819094748.png]]


## sum of all elements in a tree
![[Pasted image 20220819094826.png]]

## height of tree
![[Pasted image 20220819094937.png]]
need to recheck this pseudocode from other sources.


# count the leaf nodes and non leaf nodes
[[283.CountLeafofBinaryTreeC++.txt]]
leaf nodes are the nodes with degree 0.

## leaf nodes
if left child is null and right child is null, that is a leaf node
![[Pasted image 20220819095851.png]]


## Nodes with degree 2
![[Pasted image 20220819100024.png]]
here we are changing just the if condition.

## counting nodes with the degree 1 and 2 but not 0
![[Pasted image 20220819100151.png]]


## summary
![[Pasted image 20220819100416.png]]

4th condition can be simplified.
this looks like XOR condition

![[Pasted image 20220819100455.png]]


## Count function simplified
![[Pasted image 20220819100602.png]]

we can add if else conditions to extend this function to find other types of counts.

