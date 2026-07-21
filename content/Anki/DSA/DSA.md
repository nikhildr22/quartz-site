# DSA
STARTanki
Basic
# how to work with Input and outputs
Back: 
```cs
Console.WriteLine("Enter your name:");
string name = Console.ReadLine();
Console.WriteLine("Hello, " + name);

```
<!--ID: 1756914497202-->
ENDanki

## how do you convert to int
```cs
int age = int.Parse(Console.ReadLine());
```

## why and how to use `try parse`
```cs

int age;
bool success = int.TryParse(Console.ReadLine(), out age);
if (success)
    Console.WriteLine("You are " + age + " years old.");
else
    Console.WriteLine("Invalid input!");

```

## how do you loop through chars in a string
```cs

foreach (char c in word)
{
    Console.WriteLine(c); // Output each character
}


for (int i = 0; i < word.Length; i++)
{
    Console.WriteLine(word[i]); // Access character by index
}
```

STARTanki
TARGETanki DSA
Basic

## create a dictionary in c#

Back: 

```cs

Dictionary<char, int> romanMap = new Dictionary<char, int>()
        {
            {'I', 1}, {'V', 5}, {'X', 10},
            {'L', 50}, {'C', 100}, {'D', 500}, {'M', 1000}
        };

```



ENDanki

STARTanki
Basic
# how to convert Roman to integer

Back: 


**Lookahead Subtraction Rule**
when a smaller numeral appears before a larger one (like IV for 4 or IX for 9), it implies a subtraction. Otherwise, the Roman numerals are simply added in descending order.

```cs
public class Solution {
    public int RomanToInt(string s) {
       Dictionary<char, int> map = new Dictionary<char, int>()
       {{'I',1},{'V',5},{'X',10},{'L',50},{'C',100},{'D',500},{'M',1000}};

        int total = 0;
       for(int i=0; i<s.Length; i++){
        if(i<s.Length-1 &&map[s[i]] < map[s[i+1]]){
            total -= map[s[i]];
        }
        else{
            total += map[s[i]];
        }
       }
       return total;
    }
}
```
<!--ID: 1756914328339-->
ENDanki

## string builder
`StringBuilder` is a special class that lets you **build strings efficiently** by modifying the same object in memory.
In C#, **strings are immutable**. so any operation on string will create a copy in memory.
But with `StringBuilder`, you **cannot** use `+` directly to append. Instead, you use:

```cs
StringBuilder sb = new StringBuilder();
sb.Append("Hello");
sb.Append(" World");
```

### ⚠️ Limitations, Edge Cases & Pitfalls

- `StringBuilder` is **not thread-safe** by default.
- It’s **not needed** for small or one-time string operations.
- Overusing it in simple cases can make code unnecessarily complex.
---

# GCD or HCF and LCM

**"GCD is the biggest number that divides both. LCM is the smallest number that both divide into."**

GCD/HCF is the **largest number** that divides both numbers **without leaving a remainder**.

Let’s take two numbers: **36** and **60**

### Factors of 36:

`1, 2, 3, 4, 6, 9, 12, 18, 36`

### Factors of 60:

`1, 2, 3, 4, 5, 6, 10, 12, 15, 20, 30, 60`

### Common Factors:

`1, 2, 3, 4, 6, 12`

### Highest Common Factor (HCF) = Greatest Common Divisor (GCD) = **12**

## Euclid’s Algorithm Logic

Here’s the trick:

> Keep replacing the larger number with the remainder of dividing it by the smaller number, until the remainder becomes 0.  
> The last non-zero remainder is the GCD.



```cs

/// <summary>
    /// Calculates the Greatest Common Divisor (GCD) using Euclid's Algorithm.
    /// </summary>
    public static int GCD(int a, int b)
    {
        // Ensure both numbers are positive
        a = Math.Abs(a);
        b = Math.Abs(b);

        // Euclid's algorithm works regardless of order
        while (b != 0)
        {
            int temp = b;
            b = a % b;
            a = temp;
        }

        return a;
    }

```

Let’s say you want to find the **GCD of 18 and 48**.

You might wonder:

> “Should I pass the bigger number first?”

The answer is: **It doesn’t matter.**  
The algorithm **automatically adjusts** the values using the modulo operation.

# Divide and Conquer

# Sum of array using recursion

you need to pass the array and changing index recursively.
✅ The **base case** in recursion is the condition where the function **stops calling itself**.  
In the case of summing an array, we stop when we've **gone through all the elements**.

```cs

/// <summary>
    /// Recursively calculates the sum of an array.
    /// </summary>
    public static int Sum(int[] arr, int index = 0)
    {
        // Base case: if index reaches end of array
        if (index == arr.Length)
            return 0;

        // Recursive case: current element + sum of rest
        return arr[index] + Sum(arr, index + 1);
    }

```

# Count items in a array using recursion

similar to sum of array
```cs

static int CountItems(int[] array, int index)
    {
        // Base case: if index reaches array length, stop
        if (index == array.Length)
            return 0;

        // Recursive case: count current item + rest
        return 1 + CountItems(array, index + 1);
    }

```

# Max element in  array using recursion
```cs

static int FindMax(int[] array, int index)
    {
        // Base case: only one element left
        if (index == array.Length - 1)
            return array[index];

        // Recursive case: find max in rest of array
        int maxInRest = FindMax(array, index + 1);

        // Compare current element with max of rest
        
		// Manual comparison without Math.Max
        if (array[index] > maxInRest)
            return array[index];
        else
            return maxInRest;
	}

```
# GCD using recursion

```latex
GCD(a,b) = GCD(b, a mod  b)
```

```cs

// Recursive Divide and Conquer method to find GCD
    static int FindGCD(int a, int b)
    {
        // Base case: stop when b becomes 0
        if (b == 0)
            return a;

        // Recursive case: keep reducing the problem
        return FindGCD(b, a % b);
    }

```


# Merge sort

Merge sort uses divide and conquer.
1. Divide the array into 2 parts recursively
2. Get boths sorted via recursion
3. Then merge the sorted parts

## how do you merge the arrays?
create new array with size `size(arr1) + size(arr2)`
start from 0 index on both arrays
compare and check which is smaller, if small  - insert into new array and increment the pointer.
Do until.

```cs
static int[] mergeSort(int[] arr) {
        if (arr.length == 1) {
            return arr;
        }

        int mid = arr.length / 2;

        int[] left = mergeSort(Arrays.copyOfRange(arr, 0, mid));
        int[] right = mergeSort(Arrays.copyOfRange(arr, mid, arr.length));

        return merge(left, right);
    }
    
private static int[] merge(int[] first, int[] second) {
        int[] mix = new int[first.length + second.length];

        int i = 0;
        int j = 0;
        int k = 0;

        while (i < first.length && j < second.length) {
            if (first[i] < second[j]) {
                mix[k] = first[i];
                i++;
            } else {
                mix[k] = second[j];
                j++;
            }
            k++;
        }

        // it may be possible that one of the arrays is not complete
        // copy the remaining elements
        while (i < first.length) {
            mix[k] = first[i];
            i++;
            k++;
        }

        while (j < second.length) {
            mix[k] = second[j];
            j++;
            k++;
        }

        return mix;
    }
```

# Merge sort without extra array

```cs
static void mergeSortInPlace(int[] arr, int s, int e) {
        if (e - s == 1) {
            return;
        }

        int mid = (s + e) / 2;

        mergeSortInPlace(arr, s, mid);
        mergeSortInPlace(arr, mid, e);

        mergeInPlace(arr, s, mid, e);
    }

    private static void mergeInPlace(int[] arr, int s, int m, int e) {
        int[] mix = new int[e - s];

        int i = s;
        int j = m;
        int k = 0;

        while (i < m && j < e) {
            if (arr[i] < arr[j]) {
                mix[k] = arr[i];
                i++;
            } else {
                mix[k] = arr[j];
                j++;
            }
            k++;
        }

        // it may be possible that one of the arrays is not complete
        // copy the remaining elements
        while (i < m) {
            mix[k] = arr[i];
            i++;
            k++;
        }

        while (j < e) {
            mix[k] = arr[j];
            j++;
            k++;
        }

        for (int l = 0; l < mix.length; l++) {
            arr[s+l] = mix[l];
        }
    }
```

# Quick sort
Better than merge sort, because it does not uses extra temporary array.

1. pick a pivot, any element
	1. place it in its correct place on array
2. smaller on left and greater on right
3. do it recursively

## how do we know where to keep the pivot? how do we find out the correct place to place the pivot

we take 2 pointers left and right, and move towards the middle of the array until we find an item that violates condition (not sorted), if so, swap those 2 elements.

```
function quickSort(arr, low, high):
    if low >= high:
        return

    pivot = arr[(low + high) / 2]
    left = low
    right = high

    while left <= right:
        while arr[left] < pivot:
            left++
        while arr[right] > pivot:
            right--

        if left <= right:
            swap(arr[left], arr[right])
            left++
            right--

    quickSort(arr, low, right)
    quickSort(arr, left, high)

```

```cs
using System;

class QuickSortExample
{
    static void Main()
    {
        int[] arr = { 5, 4, 3, 2, 1 };
        QuickSort(arr, 0, arr.Length - 1);
        Console.WriteLine(string.Join(", ", arr));
    }

    static void QuickSort(int[] nums, int low, int high)
    {
        if (low >= high)
            return;

        int left = low;
        int right = high;
        int pivot = nums[low + (high - low) / 2]; // Middle element as pivot

        while (left <= right)
        {
            // Move left pointer until we find an element >= pivot
            while (nums[left] < pivot)
                left++;

            // Move right pointer until we find an element <= pivot
            while (nums[right] > pivot)
                right--;

            // Swap if needed
            if (left <= right)
            {
                int temp = nums[left];
                nums[left] = nums[right];
                nums[right] = temp;
                left++;
                right--;
            }
        }

        // Recursively sort the two halves
        QuickSort(nums, low, right);
        QuickSort(nums, left, high);
    }
}
```


# Graph basics

nodes and edges
1. Undirected graph
2. Directed graph
	1. edges will be having direction
	2. traversal is restricted by the direction mentioned in edge.

## detecting cycles in a graph
its called cyclic if there's a possibility of a path starting and ending at same node.
1. Undirected cyclic graph
2. directed cyclic graph

## what is a path?
it contains a lot of nodes and edges, and each of them are reachable.

NOTE: Node can be traversed only once in a path. aka node can not appear twice in a path.
![[Pasted image 20250917194742.png]]


## Degree in graph
for an undirected graphs, number of edges attached to a graph.
==Total degree is 2x of number of edges in a Undirected graph. This is an important property.==

For directional graph, there are 2 types of degrees
1. Indegree
2. outdegree

## Edge weight
Weight assigned to each edge.
If weights are not given, we assume them as 1.

## Data structure to store a graph
There's be given n nodes and m edges. They'll also specify if the graph is directed or undirected.

![[Pasted image 20250917195809.png]]

Also m number of lines to represent edges:
![[Pasted image 20250917195920.png]]
note that for a undirected graph, m can be any number, there's no pattern.

##

# BFS - breadth first search
you need to know these for graph traverals
breadth = level wise
you visit first level items
then level 2 items
and so on until you find the destination.


You need a queue