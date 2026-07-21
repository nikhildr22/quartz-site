# How recursion uses stack
for every function to execute, an activation record is created inside the stack.

once the function execution completes, the activation record gets deleted.
![[Pasted image 20220228094348.png]]

## Memory consumed
size of variables used inside each call multiplied by number of calls.

in this example it used N+1 calls, --> O(n) as space complexity.

![[Pasted image 20220228094758.png]]
this also consumes same memory as previous example.
