![[Pasted image 20220731051038.png]]

ADT is data and operations on a data structure.

for data representation, we need syntax to create array, size of array and length of an array.



## Linear search
How to improve linear search:
![[Pasted image 20220731053532.png]]

## Binary Search
it requires a sorted array,
low, high, mid=(low+high)/2

we'll stop when low is greater than high

![[Pasted image 20220731054147.png]]
can be implemented using loop and recursion both.

note that above recursion is tail recursion,  thus it can be easily converted into loop. 

### get set and max min of an array
- [ ] find code snippets ### get set and max min, sum, sum using recursion of an array

- [ ] ![[Pasted image 20220731061253.png]] find the code snippets
reversing 2 methods of reversing:
take auxilarry array, and copy twice back and forth.
 using a for loop twice.
![[Pasted image 20220731061448.png]]

another method is swapping first and last indices on the same array.
![[Pasted image 20220731061551.png]]
- [ ] check if u can initialize 2 variables i, j inside for loop

Left shift vs Rotate:
rotate avoids overflow and copies the overflown element to the other end.

example: LED display boards

## check if array is sorted
![[Pasted image 20220731061821.png]]
1. Inserting inside a sorted array
![[Pasted image 20220731062018.png]]
here its normal to think that we need to find the postion first, then move the elements to the right and then insert.
But this sequence of operations is computationally expensive, Thus, we'll move first, and then we insert at the desired position using this algorithm.

2. To find if Sorted.
check if 2 consecutive elements are in order.
do this for whole array.
![[Pasted image 20220731062303.png]]

3. All negative numbers on left side of array
![[Pasted image 20220731062709.png]]




## Merging 2 sorted arrays
![[Pasted image 20220731063102.png]]
note the we are using post increment operators here.

## Set operations on Array
1. union
2. intersection
3. diffference
4. set membership

### if elements of the set are not sorted
- first copy all elements of first set, the while copying the second set, we need to search in the first set so that we dont have any duplicate items.
Thus, this require n square time complexity.
![[Pasted image 20220804093735.png]]

### If set items are sorted
- union can be performed using the logic of merging sorted arrays.
![[Pasted image 20220804093833.png]]

## Intersection of 2 sets
### if sets are not sorted
- search if elements are present in other array as well
![[Pasted image 20220804094556.png]]


### if set is sorted
- we can use the logic similar to mering
- start with 0
- compare elements at 0th position
- if both are equal, copy that element into 3rd array
- if i>j, increment j
- if j>i, increment i
- compare `a[i]` with `b[j]`
- repeat the previous steps till we reach the last element.

![[Pasted image 20220804095013.png]]

## Difference of sets
for unsorted lists:
copy the elements that are not existing on other array.
![[Pasted image 20220804095157.png]]

for sorted lists:
- this is similar to merging and intersection
- start with 0
- compare elements at 0th position
- if both are equal, dont copy, increment both i,j
- if i>j, increment j, dont copy anything
- if j>i, increment i, copy `a[i]`
- compare `a[i]` with `b[j]`
- repeat the previous steps till we reach the last element.

this comparing and move ahead works because, if we move ahead, for sure we'll be reaching the next higher number.
![[Pasted image 20220804095733.png]]

## set membership
- its same as search operation.


## Student Challenge : Finding Single Missing Element in an Array
Note: first number, last number cant be missing elements.
and we also know the number of given elements
### if array is sorted
#### Array of natural numbers
using sum of first N natural numbers.

1. get the sum of all known elements
2. subtract it from the sum of n natural numbers
![[Pasted image 20220814094645.png]]

#### if elements are not first n natural numbers
we should know the first and last number for this method.
1. subtact the niumber with the respective index.
2. The difference should be same for all numbers as they are sorted
3. WHen we get a different difference, we'll stop the search if only one element was missing
4. if multiple elements are missing, we'll continue our search

![[Pasted image 20220814095102.png]]
--> in this example, the difference was different at 6th index, so we'll add the common difference that other elements had with the index number.
so, 6+6=12 is the missing element.
![[Pasted image 20220814095442.png]]

this is order of n time complexity.

### multiple missing elements in sorted array
![[Pasted image 20220814095916.png]]
the while loop is used to see if multiple elements are missing.


### Unsorted array

## A faster approach to find the missing element
![[Pasted image 20220814100521.png]]
we'll take another array.
the size of the second array will be equal to the last element of the first array.
all elements are intialized to 0.

we'll go through the first array, and increment the respective index of the second array.
at the end, we'll loop through 2nd array from low to high of 1st array, and print the missing element.

This method is also similar to Hashing.
Here sincce we are taking an array of size very large (depending on the input data we have), if memory is not the constraint, this approach is better.

## Finding Duplicates in a sorted array
in a sorted array, 
use a temp variable to store the repeated element as we traverse through the array.
repeated element is obtained by comparing 2 adjacent elements.
if they found to be equal, we'll store it in the temp.
before chaning the value of this temp variable, we'll print the value.
In this way, we can print all duplicates in a sorted array.
this continues until we traverse through all elements.

![[Pasted image 20220814101404.png]]
![[Pasted image 20220814101532.png]]

### How to count the duplicates
we'll use another counter variable.
this variable will be zero initially.
when a new duplicate is found, the counter is incremented.
when a different duplicate is found, counter is reset to 0 and temp variable is replaced with new duplicate.


![[Pasted image 20220814101924.png]]
--> this solution is using different logic than mine
time is o(n) and the while loop is negligible as we are skipping those elements later for the further tarversal of first loop.



## Finding Duplicates in a sorted array using Hashing

![[Pasted image 20220814120035.png]]
![[Pasted image 20220814120146.png]]
here we can see that we dont even have to worry about comparing the elements within the first array.
just increment the element at that particular index.
later print all the elements whos count was greater than 1.

I guess we can do the same for missing elements by printing the elements with count=0.

## Finding duplicates in an unsorted array
![[Pasted image 20220814125526.png]]
### another method is by using hashtable
![[Pasted image 20220814125956.png]]

## Finding a pair of elements with sum k
![[Pasted image 20220814155539.png]]
### Faster method with hashing
![[Pasted image 20220814155939.png]]

## Finding a pair of elements with sum k in a sorted array
![[Pasted image 20220814160510.png]]

this is more like converging from both ends of array.

## Finding min and max in a single scan
![[Pasted image 20220814160902.png]]



