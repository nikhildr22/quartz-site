# intro to strings
![[Pasted image 20220815093431.png]]

everything in computer is binary.
so the characters are defined in Ascii codes and stored and processed in the computer.

Ascii codes are for english.
Unicode is for multilanguages.

All ASCII Codes --> 0 to 127
This 7 bits are enough. But for efficient memory handling, the are stored in a byte.

Upper case -> 65 to 90
Lower case -> 97 to 122
numerics from 0 to 9 --> 48 to 57

enter key --> 10
space -> 13
escape -> 27

and all special characters have ASCII code.

Unicodes are 2 Bytes in length.
16 bits.
they are represented in 4 numbers.

## Character
this should be in sigle quote and have only one sigle value inside the quotes.

![[Pasted image 20220815094212.png]]

## Character array
![[Pasted image 20220815094427.png]]
Ways of initializing a character array.

## string
string is an array of characters.
but the end of the string is string delimitter/ null character.
in c/C++ only have this null character in strings, in other languages like Java, length of string is a property of the string and is always known.

![[Pasted image 20220815094834.png]]

Difference between the array of characters and strings is the null character at the end of the array.

## declaring and initializing the string in c/c++
![[Pasted image 20220815095029.png]]

## reading and writing a string
![[Pasted image 20220815095254.png]]

Note that this can only read single word.

Thus we need to use `gets()` function to read complete line.

words seperated by any kind of space, like newline or single space are treated as seperate strings.
But when we use `gets()` the whole line is treated as a string.

# Finding the length of the string
loop through the char array and stop when we encounter null character `\0`
![[Pasted image 20220815095740.png]]

## changing the case of the string

difference between the characters in 32.

To get Upper case, subtract 32.
to get lower case, add 32.
![[Pasted image 20220815101011.png]]

![[Pasted image 20220815100951.png]]

### How to toggle between upper and lower cases in a single go?
![[Pasted image 20220815101144.png]]


# counting words, vowels, consonents in a string
## counting vowels and consonents
![[Pasted image 20220815101503.png]]

## counting number of spaces.
count the number of spaces and add +1.
![[Pasted image 20220815101602.png]]

The above logic will fail if there are multiple consecutive spaces, thus we need to add one more condition.
![[Pasted image 20220815101750.png]]

# Validating a string
making sure only specific characters are allowed inside a string
![[Pasted image 20220815102136.png]]

# reversing a string
## using second array
![[Pasted image 20220815102330.png]]

## we'll modify the same string
make sure the language supports string as mutable for this method.
![[Pasted image 20220815102516.png]]

# comparing strings and checking palindrome
![[Pasted image 20220815103023.png]]

## checking if its a palindrome
reverse the string, and compare that with original.


Another method is by using same array, start comparing first and last elements jusk like binary search.

# Finding duplicates in a string

## by comparing with other letters
This is just like finding duplicates in an array by comparison.

## Using hashtable for counting
we need the highest ascii code of our string.
in this example we already knew our string just has lower case letters, thus we are reducing the length of hashing array by following this method.
![[Pasted image 20220815103823.png]]
we've subtracted every ascii value by 97 since we knew they all were lower case letters.
due to this, instead of taking an array from 0 to 122, we are taking array from 0 to 25, and saving some space.

loop through the array and increment that particular index for every letter.
Then print the count by adding 97 to the index of 2nd array.

![[Pasted image 20220815104141.png]]
time complexity is O(n)


## Using Bitwise operator

### Bit manipulation
[[Bit Manipulation|bit manipulation tricks]]

1. left shift
2. right shift
3. and
4. or
5. merging
6. masking

masking is knowing if a particular bit is On or OFF.

this is done by left shift and then Anding.


merging, setting another bit.
This is done by left shift and ORing.

### Finding duplicates in a string

![[Pasted image 20220815110846.png]]

in this example we knew all are lower case letters, so, we'll take an long int, which is 4 bytes long.
4 byted variable because we need 26 places for counting all possible letters.

we'll perform masking and check if answer is greater than 0, if yes then its  a duplicate.

else, we'll merge it and make that place as 1.

# Checking if 2 strings are Anagram

Anagram is a string made up a same set of alphabets.
1. they have to be equal in size
2. all letters in first string should also be present in 2nd string and vice versa.
we can do this by comparing both arrays twice.
its order is n square.

another method is by using hashtable.

![[Pasted image 20220815111732.png]]

hashing method takes o(n)
![[Pasted image 20220815112005.png]]
![[Pasted image 20220815112018.png]]


# Permutations of a string
#rewatch 
## using backtracking and recursion

Getting all arrangement of characters
n! permutations can be obtained for string of n characters.

![[Pasted image 20220815113218.png]]

in this method we are using backtracking.
in the first tree, after finding ABC, we are going back and finding ACB and so on.
This process of going back is called backtracking.

Also since we are going through all possible solutions and also backtracking, we are using bruteforce as well.

==And also, wherever we have backtracking, we can use recursion==

state space tree : A tree showing all various possible results.


we need two arrays, one for result and one for tracking which one is already repeated.

![[Pasted image 20220815115939.png]]
![[Pasted image 20220815120506.png]]

## 2nd method
using swapping
![[Pasted image 20220815120723.png]]
