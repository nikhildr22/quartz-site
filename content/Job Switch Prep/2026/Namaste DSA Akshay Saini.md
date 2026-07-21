# which langauge
DSA is language agoinistic
DSA is about problem and approach and time and space complexity.
he'll be using Js for solving problems.

# warmup
its basically programming 101, mainly in Js

# programming 101
this is level 0 of DSA

in js 3 main data types:
string number and boolean
`true` and `false` are keywords for boolean, and are case sensitive

we can use `const` and `let` keywords for defining variables in js.
diffference between `const` and `let`.

`let` can be modified later. `const` cant be.

we mostly will be using `let` .

`//` use this for comment.

NOTE:
in Js string will be converted to number if we add a string to number
![[Pasted image 20251225164218.png]]

## arrays in js
anything between square brackets is list in js.
same as any other languages.

when we try to access anything out of range, we'll get `undefined` as result.
```js
let a = [1, 2, 3, '3']
console.log(a[6])
```

here array can store any datatype. string number boolean, anything in js.

Note: ==array can also store another array, so it literally can store anything inside a list.==

## arrays in csharp
1. zero indexed

```cs
using System;

public class ArrayDemonstration
{
    public void Execute()
    {
        // 1. Single-Dimensional Array
        // Allocated on the heap with exactly 3 slots.
        string[] servers = new string[3]; 
        servers[0] = "Web-01";
        servers[1] = "Db-01";
        servers[2] = "Cache-01";
        
        // Inline initialization
        int[] ports = { 80, 443, 8080 }; 

        // 2. Multi-Dimensional (Rectangular) Array
        // A rigid 2x3 grid. Requires exactly 6 elements.
        int[,] matrix = new int[2, 3] 
        {
            { 1, 2, 3 }, // Row 0
            { 4, 5, 6 }  // Row 1
        };
        int value = matrix[1, 2]; // Accesses the '6'

        // 3. Jagged Array (Array of Arrays)
        // The parent array holds 2 elements (which are themselves array pointers)
        int[][] jagged = new int[2][]; 
        
        // Each child array can be completely different sizes
        jagged[0] = new int[2] { 10, 20 };       
        jagged[1] = new int[4] { 30, 40, 50, 60 }; 
        
        int jaggedValue = jagged[1][2]; // Accesses the '50'
    }
}
```



## creating objects in Js
object is basically a kvp - key value pairs
```js
let obj = {
	a:2,
	b:"dsds",
	c:true
}
```

arrays used index to access its elements, but in objects we can use keys to access its elements.
we'll use `.` dot operator to access its items.


csharp example:
```cs
// Creating the object
var obj = new 
{ 
    a = 2, 
    b = "dsds", 
    c = true 
};

// Accessing via dot operator
Console.WriteLine(obj.a); // Output: 2
Console.WriteLine(obj.b); // Output: dsds

// obj.a = 5; // ERROR: Anonymous types are read-only in C#
```

## 🔄 Method 2: ExpandoObject (The Behavior Match)

If you need true JavaScript-like behavior where you can add, modify, or remove properties at runtime using the dot operator, you use the `dynamic` keyword combined with `System.Dynamic.ExpandoObject`.

C#

```cs
using System.Dynamic;

// Declare as dynamic to bypass compile-time type checking
dynamic obj = new ExpandoObject();

// Add properties on the fly just like JavaScript
obj.a = 2;
obj.b = "dsds";
obj.c = true;

// Access and modify via dot operator
obj.a = 10; 
Console.WriteLine(obj.a); // Output: 10
```

## 🗂️ Method 3: Dictionary (The True Key-Value Match)

If your primary goal is specifically maintaining a collection of Key-Value Pairs (KVPs) where the keys are dynamic strings, C# uses `Dictionary<TKey, TValue>`. However, you access elements using the indexer `["key"]` rather than the dot operator.

C#

```cs
using System.Collections.Generic;

var obj = new Dictionary<string, object>
{
    { "a", 2 },
    { "b", "dsds" },
    { "c", true }
};

// Accessing via indexer (string key)
Console.WriteLine(obj["a"]); // Output: 2

// Modifying existing or adding new KVPs
obj["a"] = 99;
obj["newKey"] = "Added later";
```

## functions in js
we use `function` keyword to create a function/method

```js
function printHello() {
    console.log('hee')
}

printHello();
```

note that we dont need function `keyword` in ts.

we can also return a value from a function

```js
function sum(a, b) {
    return a+b
}

let a = sum(1, 232);
console.log(a)
```

```cs
// JS: function printHello()
public static void PrintHello() 
{
    Console.WriteLine("hee");
}

PrintHello();

// JS: function sum(a, b)
public static int Sum(int a, int b) 
{
    return a + b;
}

int a = Sum(1, 232);
Console.WriteLine(a);
```

## IF Else
same as other languages

we can use `mod` operator to get reminder (`%`).

To check if number is even
`x % 2 == 0` reminder should be 0 when devided by 2 for an even number.

## Loops

```js
for (let i = 0; i < 30; i++){
    console.log(i);
}
```
for loop has 3 elemets, `initialization` - `condition` - `change`

```cs
// JS: for (let i = 0; i < 30; i++)
for (int i = 0; i < 30; i++)
{
    Console.WriteLine(i);
}

// Infinite loop example
for (int i = 0; i > 0; i = i + 2)
{
    Console.WriteLine(i * i * i);
}
```

### different types of for loop in Js
| **Loop Type**    | **Iterates Over**         | **Returns**       | **General Syntax**          | **Maintains Order?**                              | **Best Use Case**            |
| ---------------- | ------------------------- | ----------------- | --------------------------- | ------------------------------------------------- | ---------------------------- |
| **`for`**        | Ranges / Arrays           | Index ($i$)       | `for (let i=0; i<n; i++)`   | **Yes** (Numeric)                                 | Complex logic or counting    |
| **`for...of`**   | Iterables                 | Value             | `for (const v of arr)`      | **Yes** (Sequence)                                | Simple array iteration       |
| **`for...in`**   | Objects                   | Key               | `for (const k in obj)`      | **No** (Unreliable)                               | Inspecting object properties |
| **`forEach()`**  | Arrays                    | Value & Index     | `arr.forEach((v, i) => {})` | **Yes** (Sequence)                                | Functional-style execution   |
| **JS Loop Type** | **C# Equivalent**         | **Iterates Over** | **Maintains Order?**        | **Best Use Case**                                 |                              |
| `for`            | `for`                     | Index (`i`)       | Yes                         | Complex logic, stepping, or counting.             |                              |
| `for...of`       | `foreach`                 | Value             | Yes                         | Simple array/collection iteration.                |                              |
| `for...in`       | Reflection / Dictionaries | Keys / Properties | No                          | Inspecting object properties or dictionary keys.  |                              |
| `forEach()`      | `List<T>.ForEach()`       | Value             | Yes                         | Functional-style execution on Lists (not arrays). |                              |
### Infinite loops
```js
for (let i = 0; i > 0; i=i+2){
    console.log(i*i*i);
}
```

### Looping through an array
you can use indices to loop through an array
```js
let arr = [1, 3, 4];
console.log(arr.length)

for (let i = 0; i < arr.length; i++){
    console.log(arr[i]);
}
```

```cs
// JS: let arr = [1, 3, 4];
int[] arr = { 1, 3, 4 };
Console.WriteLine(arr.Length);

for (int i = 0; i < arr.Length; i++)
{
    Console.WriteLine(arr[i]);
}
```
### Print even numbers in array
```js
let a = [1, 3, 4];
// console.log(a.length)

for (let i = 0; i < a.length; i++){
    if (a[i] % 2 == 0) {
        console.log(a[i]);
    }
}
```

```cs
int[] a = { 1, 3, 4 };

for (int i = 0; i < a.Length; i++)
{
    if (a[i] % 2 == 0) 
    {
        Console.WriteLine(a[i]);
    }
}
```
### While loop
we need to define the initial condition outside the loop.
on each iteration, the condition is checked.
increment/decrement/change is done within the loop.

```js

let i = 0;
while (i < 5) {
    console.log(i);
    i++;
}
```

```cs
int i = 0;
while (i < 5) 
{
    Console.WriteLine(i);
    i++;
}
```
### search an element in array and return its index, if not present return -1

```js
function search(arr, item) {
    for (let i = 0; i < arr.length; i++){
        if (arr[i] == item) {
            return i;
        }
    }
    return -1;
}

let arr = [1, 3, 5];
console.log(search(arr, 4))
```

```cs
public static int Search(int[] arr, int item) 
{
    for (int i = 0; i < arr.Length; i++)
    {
        if (arr[i] == item) 
        {
            return i;
        }
    }
    return -1;
}

int[] searchArr = { 1, 3, 5 };
Console.WriteLine(Search(searchArr, 4)); // Prints -1
```
### return the number of negative numbers in an array

```js
function countNegative(arr) {
    let count = 0;
    for (let i = 0; i < arr.length; i++){
        if (arr[i] < 0) {
            count++;
        }
    }
    return count;
}

let arr = [-1, -3, 5];
console.log(countNegative(arr))
```

```cs
public static int CountNegative(int[] arr) 
{
    int count = 0;
    for (int i = 0; i < arr.Length; i++)
    {
        if (arr[i] < 0) 
        {
            count++;
        }
    }
    return count;
}

int[] negArr = { -1, -3, 5 };
Console.WriteLine(CountNegative(negArr)); // Prints 2
```
### returns the largest number in an array
```js
function returnLargest(arr) {
    let largest = arr[0];
    for (let i = 0; i < arr.length; i++){
        if (arr[i] > largest) {
            largest = arr[i]
        }
    }
    return largest;
}

let arr = [11, 3, 5];
console.log(returnLargest(arr))
```

we have ==`Infinity`== keyword in js.
C# is statically typed, you access infinity through the type you are using (usually `double` or `float`)
 
| **JavaScript** | **C# (double)**           | **C# (float)**           |
| -------------- | ------------------------- | ------------------------ |
| `Infinity`     | `double.PositiveInfinity` | `float.PositiveInfinity` |
| `-Infinity`    | `double.NegativeInfinity` | `float.NegativeInfinity` |

```cs
double result = 1.0 / 0.0;

// Method 1: Comparison
if (result == double.PositiveInfinity) { ... }

// Method 2: Recommended Helper Methods
if (double.IsInfinity(result)) { ... }         // True for both + and -
if (double.IsPositiveInfinity(result)) { ... } // True only for +
```


```js
function returnLargest(arr) {
    let largest = -Infinity;
    for (let i = 0; i < arr.length; i++) {
        if (arr[i] > largest) {
            largest = arr[i]
        }
    }
    return largest;
}

let arr = [-11, -3, -5];
console.log(returnLargest(arr)) // prints -3
```

### Find smallest
```js
function returnSmallest(arr) {
    let smallest = Infinity;
    for (let i = 0; i < arr.length; i++) {
        if (arr[i] < smallest) {
            smallest = arr[i]
        }
    }
    return smallest;
}

let arr = [-11, -3, -5];
console.log(returnSmallest(arr)) // returns -11
```

## 📈 Min/Max & The "Infinity" Concept

In JavaScript, arrays are untyped and you use `-Infinity` or `Infinity`. In C#, arrays are typed.

- For `int[]` arrays, you use `int.MinValue` and `int.MaxValue`.
    
- For `double[]` arrays, you use `double.NegativeInfinity` and `double.PositiveInfinity`.
    

### Return Largest Number (Using `int.MinValue`)


```cs
public static int ReturnLargest(int[] arr) 
{
    // C# equivalent of -Infinity for integers
    int largest = int.MinValue; 
    
    for (int i = 0; i < arr.Length; i++) 
    {
        if (arr[i] > largest) 
        {
            largest = arr[i];
        }
    }
    return largest;
}

int[] largestArr = { -11, -3, -5 };
Console.WriteLine(ReturnLargest(largestArr)); // Prints -3
```

### Return Smallest Number (Using `int.MaxValue`)


```cs
public static int ReturnSmallest(int[] arr) 
{
    // C# equivalent of Infinity for integers
    int smallest = int.MaxValue; 
    
    for (int i = 0; i < arr.Length; i++) 
    {
        if (arr[i] < smallest) 
        {
            smallest = arr[i];
        }
    }
    return smallest;
}

int[] smallestArr = { -11, -3, -5 };
Console.WriteLine(ReturnSmallest(smallestArr)); // Prints -11
```

**Pro-Tip:** ⚠️ Avoid writing manual `for` loops for basic array searches in production C#. Utilize the built-in LINQ library to achieve this declaratively (e.g., `arr.Max()` or `Array.IndexOf(arr, 4)`), which is highly optimized at the runtime level.

## Find the 2nd largest
before writing code, write a pseudocode on paper and then move on to writng code.
Here we need to track 2 numbers.
Pseudo code:
1. Loop
	1. If number is greater than 1st Largest
		1. ==Update second largest with prev first largest value==
		2. Update first largest
	2. Else if number is greater than 2nd largest
		1. update 2nd largest
2. return 2nd largest

```js
function findSecondLargest(arr) {
    let firstLargest = -Infinity;
    let secondLargest = -Infinity;
    for (let i = 0; i < arr.length; i++){
        if (arr[i] > firstLargest) {
            secondLargest = firstLargest;
            firstLargest = arr[i];
        }
        else if (arr[i] > secondLargest) {
            secondLargest = arr[i];
        }
    }
    return secondLargest;
}

let arr = [-11, -3, -5, 2];
console.log(findSecondLargest(arr))
```

```cs
using System;

public class ArrayAlgorithms
{
    public static int FindSecondLargest(int[] arr) 
    {
        // C# equivalent of -Infinity for integers
        int firstLargest = int.MinValue;
        int secondLargest = int.MinValue;
        
        for (int i = 0; i < arr.Length; i++)
        {
            if (arr[i] > firstLargest) 
            {
                secondLargest = firstLargest;
                firstLargest = arr[i];
            }
            else if (arr[i] > secondLargest) 
            {
                secondLargest = arr[i];
            }
        }
        
        return secondLargest;
    }

    public static void Main()
    {
        int[] arr = { -11, -3, -5, 2 };
        Console.WriteLine(FindSecondLargest(arr)); // Output: -3
    }
}
```

Edge cases:
==if array length is less than 2, return null.==

==what if there are duplicate numbers?== add this additional conditional check before updating the secondLargest number
```js
else if (arr[i] > secondLargest && arr[i] != firstLargest) {
            secondLargest = arr[i];
        }
```


```js
function findSecondLargest(arr) {
    if (arr.length < 2) {
        return null;
    }
    let firstLargest = -Infinity;
    let secondLargest = -Infinity;
    for (let i = 0; i < arr.length; i++){
        if (arr[i] > firstLargest) {
            secondLargest = firstLargest;
            firstLargest = arr[i];
        }
        else if (arr[i] > secondLargest && arr[i] != firstLargest) {
            secondLargest = arr[i];
        }
    }
    return secondLargest;
}

let arr = [-11, -66, -11, -12];
console.log(findSecondLargest(arr))
```

```cs
using System;

public class ArrayAlgorithms
{
    // Note the int? return type, allowing the method to return null
    public static int? FindSecondLargestWithEdgeCases(int[] arr) 
    {
        // Edge Case 1: Array length is less than 2
        if (arr == null || arr.Length < 2) 
        {
            return null;
        }
        
        int firstLargest = int.MinValue;
        int secondLargest = int.MinValue;
        
        for (int i = 0; i < arr.Length; i++)
        {
            if (arr[i] > firstLargest) 
            {
                secondLargest = firstLargest;
                firstLargest = arr[i];
            }
            // Edge Case 2: Duplicate numbers (prevent secondLargest from matching firstLargest)
            else if (arr[i] > secondLargest && arr[i] != firstLargest) 
            {
                secondLargest = arr[i];
            }
        }
        
        // Edge Case 3 (C# Specific): If the array was entirely identical duplicates (e.g., [11, 11]), 
        // secondLargest will never be updated and remains int.MinValue. 
        if (secondLargest == int.MinValue) 
        {
            return null; 
        }
        
        return secondLargest;
    }

    public static void ExecuteFinal()
    {
        int[] arr = { -11, -66, -11, -12 };
        Console.WriteLine(FindSecondLargestWithEdgeCases(arr)); // Output: -12
    }
}
```
## Common edge cases in arrays:
1. array is empty
2. array has negative numbers
3. array has duplicates
4. array has infifity numbers
Make sure you ask the interviewer these questions before you solve anything.

## 📋 Common Array Edge Cases Checklist for Interviews

Always ask the interviewer about these constraints before writing a single line of code:

- **Is the array guaranteed to be instantiated?** (Check for `null` object references in C#).
    
- **What if the array is empty or has fewer elements than required?** (Throw `ArgumentException` or return `null`).
    
- **Are negative numbers allowed?** (Determines if you initialize tracking variables at `0` or `int.MinValue`).
    
- **Are there duplicate values?** (Requires strict `>` vs `>=` evaluation).
    
- **Is the array sorted?** (If yes, you don't need a loop; just return `arr[arr.Length - 2]`).
    
- _(C# Specific)_ **Will the values exceed the 32-bit integer limit?** (Determines if you should use `int[]` or `long[]`).

[[3rd largest]]

## Loop within a Loop

This concept is used in multiple problems. sorting etc

the total iteration will be M x N times.
where M is the number of iteration of 1st loop and N is number of iterations of 2nd loop.

The below loop will be run `m x n` times, aka 50 times
```js
let m = 5;
let n = 10;
for (let i = 0; i < m; i++){
    for (let j = 0; j < n; j++){
        console.log(i, j);
    }
}
```

### How to make sure inner loop runs i number of times
```js
let m = 5;
for (let i = 0; i < m; i++) {
    for (let j = 0; j < i; j++) {
        console.log(i, j);
    }
}
```

### How to make sure inner loop runs i+1 number of times
==Note the usage of <= sign==
```js
let m = 5;
for (let i = 0; i < m; i++) {
    for (let j = 0; j <= i; j++) {
        console.log(i, j);
    }
}
```

## Star patterns
![[Pasted image 20251227134113.png]]

```js
let n = 4;
for (let i = 0; i < n; i++){
    let row = '';
    for (let j = 0; j < n; j++){
        row += '* ';
    }
    console.log(row)
}
```

```cs
using System;

public class StarPatterns
{
    public static void PrintSolidSquare(int n)
    {
        // Outer loop: Rows (Y-axis)
        for (int i = 1; i <= n; i++)
        {
            // Inner loop: Columns (X-axis)
            // Notice the limit is exactly 'n', completely ignoring 'i'
            for (int j = 1; j <= n; j++)
            {
                Console.Write("* ");
            }
            
            Console.WriteLine(); // Carriage return
        }
    }
}
```
## 🔲 2. The Hollow Square (Coordinate Boundaries) Interviewers will often ask you to hollow out a shape. 
You solve this by turning the grid into a strict coordinate system and using an `if/else` statement inside the inner loop. **The Boundary Logic:** You only print a star if the current coordinate touches one of the four outer walls. Otherwise, you print a blank space. * Top Wall: `i == 1` * Bottom Wall: `i == n` * Left Wall: `j == 1` * Right Wall: `j == n` ```

```csharp 
public static void PrintHollowSquare(int n) { 
	for (int i = 1; i <= n; i++) 
	{ 
		for (int j = 1; j <= n; j++) { 
			// If the coordinate touches ANY of the 4 outer walls, print a star 
			if (i == 1 || i == n || j == 1 || j == n) {
				Console.Write("* "); } 
			else {
			 // Otherwise, print hollow space inside the boundaries 
			 Console.Write(" "); } } Console.WriteLine(); 
			 } 
		 }
	 }
 }
```

## left aligned right angle triangle

```js
let n = 4;
for (let i = 0; i < n; i++){
    let row = '';
    for (let j = 0; j <= i; j++){
        row += '* ';
    }
    console.log(row)
}
```

```cs
using System;

public class StarPatterns
{
    public static void Main()
	{
		int n = 5;
		for(int i=0;i<n;i++){
			for(int j=0;j<i+1;j++){
			 Console.Write("* ");	
			}
			Console.WriteLine();
		}
	}
}
```


![[Pasted image 20251227134912.png]]

```js
let n = 4;
for (let i = n; i > 0; i--){
    let row = '';
    for (let j = 0; j < i; j++){
        row += '* ';
    }
    console.log(row)
}
```

```cs
public static void Main()
	{
		int n = 5;
		for(int i=n;i>0;i--){
			for(int j=0;j<i;j++){
			 Console.Write("* ");	
			}
			Console.WriteLine();
		}
	}
```

![[Pasted image 20251227135146.png]]

```js
let n = 5;

for (let i = 1; i <= n; i++){
    let row = '';
    for (let j = 1; j <= i; j++){
        row += j + ' ';
    }
    console.log(row)
}
```

```cs
public static void Main()
	{
		int n = 5;
		for(int i=0;i<n;i++){
			for(int j=1;j<i+2;j++){
			 Console.Write(j);	
			}
			Console.WriteLine();
		}
	}
```

```cs
public static void Main()
	{
		int n = 5;
		for(int i=1;i<=n;i++){
			for(int j=1;j<=i;j++){
			 Console.Write(j + " ");	
			}
			Console.WriteLine();
		}
	}
```

![[Pasted image 20251227135458.png]]

```js
let n = 5;

for (let i = 1; i <= n; i++){
    let row = '';
    for (let j = 1; j <= i; j++){
        row += i + ' ';
    }
    console.log(row)
}
```

```cs
public static void Main()
	{
		int n = 5;
		for(int i = 1; i <= n; i++){
			for(int j = 1 ; j <= i ; j++){
			 Console.Write(i + " ");	
			}
			Console.WriteLine();
		}
	}
```

![[Pasted image 20251227135601.png]]

```js
let n = 5;

for (let i = n; i > 0; i--){
    let row = '';
    for (let j = 1; j <= i; j++){
        row += j + ' ';
    }
    console.log(row)
}
```
There are different ways, this is not the only solution, just understand the intuition behind loop inside a loop
```js
let n = 5;

for (let i = 0; i < n; i++){
    let row = '';
    for (let j = 0; j <n-i; j++){
        row += j+1 + ' ';
    }
    console.log(row)
}
```

```cs
public static void Main()
	{
		int n = 5;
		for(int i=0;i<=n;i++){
			for(int j=1;j<n-i+1;j++){
			 Console.Write(j + " ");	
			}
			Console.WriteLine();
		}
	}
```
![[Pasted image 20251227135946.png]]

```js
let n = 5;

for (let i = 0; i < n; i++){
    let row = '';
    for (let j = 0; j <n-i; j++){
        row += '*' + ' ';
    }
    console.log(row)
}
```

```cs
public static void Main()
	{
		int n = 5;
		for(int i=0;i<n;i++){
			for(int j=0;j<n-i;j++){
			 Console.Write("* ");	
			}
			Console.WriteLine();
		}
	}
```

![[Pasted image 20251227140044.png]]

For this one you've to make sure there are empty spaces in the row, and number of empty spaces should decrease as the number grows.

```js
let n = 5;

for (let i = 0; i < n; i++){
    let row = '';
    for (let k = 0; k < n - (i + 1); k++){
        row += ' ';
    }
    for (let j = 0; j <=i; j++){
        row += '*' + ' ';
    }
    console.log(row)
}
```

```cs
public static void Main()
	{
		int n = 5;
		for(int i=0;i<n;i++){
			for(int j=0;j<n-i-1;j++){
			 Console.Write(" ");	
			}
			for(int j=0;j<i+1;j++){
			 Console.Write("*");	
			}
			Console.WriteLine();
		}
	}
```

![[Pasted image 20251227140928.png|592]]

==For this alternate pattern, we can introduce a switchable character and switch its values for every inner loop iteration==

```cs
public static void Main()
	{
		int n = 5;
		
		for(int i=0;i<n;i++){
			int flag = 1;
			for(int j=0;j<i+1;j++){
			 Console.Write(flag);
			 flag = flag == 0 ? 1 : 0;
			}
			Console.WriteLine();
		}
	}
```

```js
let n = 5;

for (let i = 0; i < n+1; i++){
    let row = '';
    let switchChar = 1; // THIS IS IMPORTANT - and is within the loop
    for (let j = 0; j <=i; j++){
        row += switchChar + ' ';
        switchChar = switchChar == 0 ? 1 : 0;
    }
    console.log(row)
}
```

![[Pasted image 20251227141553.png]]

Here the toggle once initialized does not need to be reset again on every first loop iteration.

==note where we are moving flag/switchchar out of loop or within the loop==

```js
let n = 5;
let switchChar = 1; // THIS IS IMPORTANT - and is outside the loop
for (let i = 0; i < n + 1; i++) {
    let row = '';
    for (let j = 0; j <= i; j++) {
        row += switchChar + ' ';
        switchChar = switchChar == 0 ? 1 : 0;
    }
    console.log(row)
}
```

```cs
public static void Main()
	{
		int n = 5;
		int flag = 1;
		
		
		for(int i=0;i<n;i++){
			for(int j=0;j<i+1;j++){
			 Console.Write(flag);
			 flag = flag == 0 ? 1 : 0;
			}
			Console.WriteLine();
		}
	}
```

### Print 5 or S pattern

```cs
using System;

public class Program
{
    public static void Main()
    {
        int n = 5;

        // Outer loop handles the rows (Height is 2 * n)
        for (int i = 0; i <= n * 2; i++)
        {
            // Inner loop handles the columns (Width is n)
            for (int j = 0; j < n; j++)
            {
                // 1. Horizontal Bars (Top, Middle, Bottom)
                if (i == 0 || i == n || i == n * 2)
                {
                    Console.Write("*");
                }
                // 2. Top-Left Vertical Wall
                else if (i < n && j == 0)
                {
                    Console.Write("*");
                }
                // 3. Bottom-Right Vertical Wall
                else if (i > n && j == n - 1)
                {
                    Console.Write("*");
                }
                // 4. Empty Space inside the boundaries
                else
                {
                    Console.Write(" ");
                }
            }
            
            // CRITICAL FIX: Move to the next line only AFTER printing the entire row
            Console.WriteLine();
        }
    }
}
```

## Count the digits in given number
==we can count the digits by finding out how many times a number  can be divided by 10==.

Note that division in Js gives decimal, so use `Math.floor`

```js
let n = 2596;
let count = 0;
while (n > 0) {
    n = Math.floor(n / 10);
    count++;
}
console.log(count); // returns 4
```

### Edge cases
1. what if n is 0
2. what if n is negative number

```js
function countDigits(n) {
    if (n == 0) {
    // egde case when number is 0
        return 1;
    }
    if (n < 0) {
    // edge case when number is negative number
        n = Math.abs(n);
    }
    let count = 0;
    while (n > 0) {
        n = Math.floor(n / 10);
        count++;
    }
    return count;
}

console.log(countDigits(-123))
```

```cs
using System;

public class NumberAlgorithms
{
    public static int CountDigits(int n)
    {
        // Edge Case 1: When the input number is exactly 0
        if (n == 0)
        {
            return 1;
        }

        // Edge Case 2: When the input number is negative
        // Math.Abs handles stripping the negative sign cleanly
        if (n < 0)
        {
            n = Math.Abs(n);
        }

        int count = 0;

        while (n > 0)
        {
            // C# automatically drops decimals during integer division
            n = n / 10; 
            count++;
        }

        return count;
    }

    public static void Main()
    {
        Console.WriteLine(CountDigits(-123)); // Output: 3
        Console.WriteLine(CountDigits(0));    // Output: 1
        Console.WriteLine(CountDigits(2596)); // Output: 4
    }
}
```
## Palidrome
an integer is a palindrome if the number is same when read from front and back.
reversed number should be same as original number.

first we should know how to reverse a number.
## 🧠 The "Conveyor Belt" Reversal Logic

To reverse a number mathematically without converting it into a string, you use a three-step loop:

1. **`n % 10`**: Grabs the last digit off the end of the number.
    
2. **`(10 * rev) + lastDigit`**: Shifts the existing reversed number to the left (multiplying by 10 makes room) and appends the new digit to the end.
    
3. **`n / 10`**: Chops the last digit off the original number.


```js
function isPalindrome(n) {
    let orig = n;
    let rev = 0;
    while (n > 0) {
        let lastDigit = n % 10;
        rev = (10 * rev) + lastDigit;
        n = Math.floor(n / 10);
    }

    if (orig == rev) {
        console.log(orig, 'Yes');
    }
    else {
        console.log(orig, 'NO');
    }
}

isPalindrome(1234);
isPalindrome(121);
```

### Egde cases
1. what if number is negative
	1. Negative  number can never be palindrome.
```js
function isPalindrome(n) {
    if (n < 0) {
        console.log(n, "NO")
    }
    let orig = n;
    let rev = 0;
    while (n > 0) {
        let lastDigit = n % 10;
        rev = (10 * rev) + lastDigit;
        n = Math.floor(n / 10);
    }

    if (orig == rev) {
        console.log(orig, 'Yes');
    }
    else {
        console.log(orig, 'NO');
    }
}

isPalindrome(1234321);
isPalindrome(-121);
```

```cs
using System;

public class PalindromeAlgorithms
{
    public static void IsPalindrome(int n)
    {
        // Edge Case: Negative numbers cannot be palindromes
        if (n < 0)
        {
            Console.WriteLine($"{n} NO");
            return;
        }

        int original = n;
        int reversed = 0;

        while (n > 0)
        {
            int lastDigit = n % 10;
            reversed = (10 * reversed) + lastDigit;
            
            // C# automatically truncates decimals during integer division
            n = n / 10; 
        }

        if (original == reversed)
        {
            Console.WriteLine($"{original} Yes");
        }
        else
        {
            Console.WriteLine($"{original} NO");
        }
    }
}
```
## Reverse integer
Here the edge case is negative numbers, so we are taking absolute value of number. and later while returning we'll assign the respective sign.
```js
function reverseInteger(n) {
    let orig = n;
    n = Math.abs(n);
    let reverse = 0;
    while (n > 0) {
        let lastDigit = n % 10;
        reverse = (10 * reverse) + lastDigit;
        n = Math.floor(n / 10);
    }

    return orig > 0 ? reverse : -(reverse);
}

console.log(reverseInteger(123));
console.log(reverseInteger(-123));
```

```cs
public static int ReverseInteger(int n)
{
    int original = n;
    
    // Convert to positive to run the algorithm safely
    n = Math.Abs(n);
    int reversed = 0;

    while (n > 0)
    {
        int lastDigit = n % 10;
        reversed = (10 * reversed) + lastDigit;
        n = n / 10;
    }

    // Ternary operator: If original was positive, return reversed. Otherwise, make it negative.
    return original > 0 ? reversed : -reversed;
}
```


## Time and space complexity
### Time complexity
its used to measure the efficiency of the algorithm in terms of speed, as input size grows.
==Note that time complexity is not equal to time taken by algorithm.==
different machines run same code at different speed.

### Big O notation
we'll represent the time complexity by its worst case.
![[Pasted image 20251227203546.png]]

### Space complexity
number of extra variables or leght of duplicate array.
single variable will be O(1)
an extra array will be O(n)
an extra 2D array will be O(n^2)

Note: if time complexity is O(3n) we usually ignore the number 3.

## Edge case for Integer
1. Int can be positive
2. Int can be negative
3. Int can be 0

# 04. Arrays - Easy & Medium

**Sorted and Non decreasing keyword is not same as strictly increasing, aka it can contain duplicated**
## remove duplicates from a sorted array

#important ==When asked to change the array inplace, we need to modify the existing array==
![[Pasted image 20260101203732.png]]



This is a 2 Pointer problem

```js
function removeDuplicates(arr) {
    let nextPositionPointer = 0;
    for (let i = 0; i < arr.length; i++) {
        if (arr[i + 1] != arr[i]) {
            let uniquePointer = i;
            arr[nextPositionPointer] = arr[uniquePointer];
            nextPositionPointer++;
        }
    }
    return arr;
}

console.log(removeDuplicates([0, 0, 1, 1, 2, 2, 3, 4, 5, 5, 5, 5, 5]));

```

### we can also reduce one more variable
```js
function removeDuplicates(arr) {
    let nextPositionPointer = 0;
    for (let i = 0; i < arr.length; i++) {
        if (arr[i] > arr[nextPositionPointer]) { // NOTE this condition will be reverse if the array is sorted in descending order
            nextPositionPointer++;
            arr[nextPositionPointer] = arr[i];
        }
    }
    return arr;
}

console.log(removeDuplicates([0, 0, 1, 1, 2, 2, 3, 4, 5, 5, 5, 5, 5]));
```

### for array sorted in descending order
```js
function removeDuplicates(arr) {
    let nextPositionPointer = 0;
    for (let i = 0; i < arr.length; i++) {
        if (arr[i] < arr[nextPositionPointer]) { // ONLY THIS CONDITION IS CHANGED
            nextPositionPointer++;
            arr[nextPositionPointer] = arr[i];
        }
    }
    return arr;
}

console.log(removeDuplicates([5, 5, 4, 3, 3, 2, 2, 1, 0]));
```

## Remove element
![[Pasted image 20260101210133.png]]

we'll use the same 2 pointer technique.
also note the we are modifying the array inplace.
```js
var removeElement = function (nums, val) {
    let nextPos = 0
    for (let i = 0; i < nums.length; i++){
        if (nums[i] != val) {
            nums[nextPos] = nums[i];
            nextPos++;
        }
    }
    return nextPos;
}

let arr = [0,1,2,2,3,0,4,2];
console.log(removeElement(arr, 2))
console.log(arr)
```

## Reverse a string given the input string is arrat of characters and modify the array inplace
![[Pasted image 20260101211914.png]]

Note that this is inplace replace.
and swapping needs a temp variable.
==NOTE that we need to iteratate through only `n / 2` times, where n is length of array==
If you iterate though entire array instead of n/2 you'll end up with same string. Tried and tested
- This N/2 works fine for both odd length and even length array
```js
var reverseStringArr = function (arr) {
    for (let i = 0; i < Math.floor(arr.length / 2); i++){
        let temp = arr[i];
        arr[i] = arr[arr.length - 1 - i]
        arr[arr.length - 1 - i] = temp;
    }
}

let arr = ['h', 'e', 'l', 'l', 'o'];
console.log(reverseStringArr(arr))
console.log(arr)
```

## Best time to Buy and Sell a stock
![[Pasted image 20260101213817.png]]

### bruter force approach
O(N^2) time complexity as we'll be finding all combinations and then finding max profit.

### smart approach
this is also 2 pointer problem
you need two pointer, one to keep min number and one max profit number

```js
var maxProfit = function (arr) {
    let profit = 0;
    let minValue = arr[0];
    for (let i = 1; i < arr.length; i++) {
        if (arr[i] - minValue > profit) {
            profit = arr[i] - minValue;
        }
        if (arr[i] < minValue) {
            minValue = arr[i];
        }
    }

    return profit;
}

let arr = [1, 1, 2, 6, 2, 3];
console.log(maxProfit(arr))
console.log(arr)
```


## Merging sorted array
![[Pasted image 20260101223351.png]]

==Note: Non Decreasing order means, its increasing order but there could be duplicates==
![[Pasted image 20260101223704.png]]


### 1st approach
this is bruteforce apprach
simply copy 2nd array to end of 1st array, and then sort
time complexity will be `O((m+n)log(m+n))` from copying and sorting

### 2nd Approach
you can create a copy of array 1