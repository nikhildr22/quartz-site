# Tail recursion
 **if the recursive call is the last statement of the recursive function** --> then it is called tailed recursion.

 ![[Pasted image 20220307091846.png]]

 if any operation is pending after recursive call, then its not a tail recursion.
 
 ![[Pasted image 20220307091809.png]]
--> here we are adding after recursion call, so it cant be a tail recursion

## tail recursion vs Loop
tail recursion can be easily converted into a loop.
and the loop is more efficient for space complexity.

![[Pasted image 20220307092101.png]]

time complexity is same. O(n)

space complexity:
 ![[Pasted image 20220307092206.png]]
 sometimes it depends on the compiler.
 to reduce the space complexity, the compiler may convert the tail recursion into a loop.
 because loop has a constant space complexity.