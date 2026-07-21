All elements on the left side of the node are smaller than that of the value of the node,
all elements on the right side of the node are greater than that of the value of the node.

we'll use BST for searching.

1. BST will not have duplicates
2. Inorder traversal of the tree gives sorted values
## Number of Binary search trees for n nodes
![[Pasted image 20220820092638.png]]
![[Pasted image 20220820092728.png]]
this is catalan number.

its more like labelled binary tree representation.

we'll use nodes data structure not array to represent BST

# searching in a Binary Search tree
![[Pasted image 20220820093048.png]]
number of comparisons is dependant on the height of the tree.

## using recursion
![[Pasted image 20220820093225.png]]

## using iterative loops
![[Pasted image 20220820093436.png]]


# Inserting in a BST
1. search if the value is already present
2. if not, insert in a respective position


we need two pointers.
one pointer is `tail` pointer

![[Pasted image 20220820093954.png]]

note that if we are not using another pointer, we have to traverse the tree once again after search to insert.


# recursively insert in BST
![[Pasted image 20220822092349.png]]

for first insertion:
![[Pasted image 20220822092501.png]]

for all upcoming insertions:
we can simply call the insert function.

This function will do insert operation recursivly and add the new node as left/right child for one of the node.


# Create a BST
![[Pasted image 20220822092850.png]]
we need to first search and then insert, thus it takes nlog(n) time complexity.

[[289.BSTInsertInorder&SearchC++]]


# deleting from the BST

![[Pasted image 20220822093711.png]]
4 Scenarios can occur when we are deleting.
1. if its a leaf node, just search and delete and modify parent node to point its deleted node to null
2. when a node with single child is deleted, the child will replace the parent node
3. if node with multiple children is deleted, its inorder predeccessor or inorder successor will replace it
	1. inorder predecessor is found by going left once and going to the right till we get null
	2. inorder successor is found by going right once and going to the left till we get null
4. when we delete and node and inorder predecessor or successor has to replace it, and the predecessor or successor has children, its predecessor or successor will replace the new vacant position, this has to be perfromed recursive until we fill all empty positions.




# generating BST from preorder
for Binary tress we needed two traversals to generate a tree.

But for BST, we need either preorder or post order we can generate a tree.


[[293.BSTfromPreorderUsingSTLStackC++.txt]]
![[Pasted image 20220822100245.png]]

for post order, we have to use similar procedure, only chnage is taht we have to start from right side of post order.


# Drawback of BST
![[Pasted image 20220822100718.png]]
The height of BST will depend on the order of insertion.
as a developer, we can only control the logic of insertion and not the order of insertion.
because insertion will be user dependant, and user can insert in any order.

Thus to solve this drawback,  we use self balanced AVL trees.

