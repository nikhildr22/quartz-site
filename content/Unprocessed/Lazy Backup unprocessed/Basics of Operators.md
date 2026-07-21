**Operators** are symbols that tell the compiler to perform specific mathematical or logical manipulations.

1. Arithmetic  
2. Relational  
3. Bitwise  
4. Logical  
5. Assignment  
6. Increment  
7. Miscellaneous

# Arithmetic  operators

1. addition
2. subtraction
3. multiplication
4. division
5. modulus
![[Pasted image 20220618073437.png]]

**Relational Operators**: These operators are used for comparison. They return either **true** or **false** based on the comparison result.

1. equal
2. not equal
3. greater than
4. less than
5. greater than or equal
6. less than or equal

![[Pasted image 20220618073426.png]]


**Bitwise Operators**:
These operators convert the given integers into binary and then perform the required operation, and give back the result in decimal representation.
1. Bitwise AND
2. Bitwise OR
3. Bitwise XOR
4. Bitwise NOT
5. left shift
6. right shift
![[Pasted image 20220618073529.png]]


**Logical Operators**: These operators take boolean values as input and return boolean values as output.  
Note: In C,C++ any non-zero number is treated as true and 0 as false but this doesn't hold for Java.


1. logical AND
2. logical OR
3. logical NOT

Assignment:
![[Pasted image 20220618073946.png]]


**Increment/Decrement Operators**: These are **unary** operators. Unary operators are the operators which require only one operand.

![[Pasted image 20220618074019.png]]


Miscelaneous operator:
**x = (condition) ? a : b**  
If condition is true,then a is assigned to x else b is assigned to x. It is a ternary operator because it uses the condition, a and b i.e. three operands (the condition is also treated as a boolean operand).

**Operator Precedence and Associativity**:  

**Precedence Rules**: The precedence rules specify which operator is evaluated first when two operators with different precedence are adjacent in an expression.  
For example: x=a+++b  
This expression can be seen as postfix increment on a and addition with b or prefix increment on b and addtion to a. Such issues are resolved by using precedence rules.  

**Associativity Rules**: The associativity rules specify which operator is evaluated first when two operators with the same precedence are adjacent in an expression.  
For example: a∗b/c

![[Pasted image 20220618074451.png]]


By default, `cin` reads from the input discarding any spaces. So, all you have to do is to use a do `while` loop to read the input more than one time:

```cpp
do {
   cout<<"Enter a number, or numbers separated by a space, between 1 and 1000."<<endl;
   cin >> num;

   // reset your variables

   // your function stuff (calculations)
}
while (true); // or some condition
```

- [ ] Learning datatypes required for constraints and limits of data types for large numbers
- [ ] difference between different c++ in online compilers
- [ ] 