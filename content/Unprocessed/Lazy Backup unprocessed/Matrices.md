We'll learn about Special matrices.
these are square matrices.
They have non zero matrices.
![[Pasted image 20220815122947.png]]

# Diagonal matrix
all elements except diagonal elemets are zero.
![[Pasted image 20220815123105.png]]

if we take nxn matrix for this one, most of the elements will be zero.
This'll waste a lot of space.
And also, during computation, we'll waste a lot of time dealing with positions that has 0.

Thus, we'll take a single dimentional array and store the non zero elements.
![[Pasted image 20220815123345.png]]

Setters and getter functions for a diagonal matrix.
![[Pasted image 20220815123608.png]]
here we are using `A[i-1]` because the matrix indices were 1 to n.


# Lower triangular matrix - Row major mapping

all elements above diagonal are 0.
i.e., if row number is less than column number, the value should be 0.
![[Pasted image 20220815124404.png]]

![[Pasted image 20220815124329.png]]

How can we store these efficiently?
## using row major method
we'll store using row by row
![[Pasted image 20220815124505.png]]

![[Pasted image 20220815124727.png]]

## using column major method
![[Pasted image 20220815124832.png]]
![[Pasted image 20220815125120.png]]

#todo/paused 