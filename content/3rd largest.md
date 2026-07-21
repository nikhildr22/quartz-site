## BLUF

**Yes, you can use the exact same logic** by introducing a third variable, but the `if/else` cascading becomes cumbersome. While manually tracking variables is the fastest approach ($O(N)$ time) for the 2nd or 3rd largest, if an interviewer asks for the 3rd, they are usually baiting you to see if you can generalize the problem to the **$K$-th Largest Element**.

## 💻 Approach 1: The Direct Extension (3 Variables)

If you strictly want to follow the previous pattern, you add a `thirdLargest` variable. When a new 1st place is found, the previous 1st gets pushed to 2nd, and the previous 2nd gets pushed to 3rd.

C#

```cs
public static int? FindThirdLargest(int[] arr)
{
    if (arr == null || arr.Length < 3) return null;

    int first = int.MinValue;
    int second = int.MinValue;
    int third = int.MinValue;

    for (int i = 0; i < arr.Length; i++)
    {
        if (arr[i] > first)
        {
            // Cascade the demotions down the line
            third = second;
            second = first;
            first = arr[i];
        }
        else if (arr[i] > second && arr[i] != first)
        {
            third = second;
            second = arr[i];
        }
        else if (arr[i] > third && arr[i] != second && arr[i] != first)
        {
            third = arr[i];
        }
    }

    return third == int.MinValue ? null : third;
}
```

## 🛑 The Interview Pivot: The $K$-th Largest Problem

If an interviewer asks for the 4th, 10th, or 100th largest number, writing 100 `if/else` statements is impossible. You must pivot your strategy.

### Method A: The LINQ Approach (Sorting)

The easiest way to read the code, but it requires sorting the entire array, giving it a time complexity of $O(N \log N)$.

C#

```cs
using System.Linq;

public static int? FindKthLargestLinq(int[] arr, int k)
{
    // Order descending, remove duplicates, skip K-1 elements, take the next one
    var result = arr.Distinct()
                    .OrderByDescending(x => x)
                    .Skip(k - 1)
                    .Cast<int?>()
                    .FirstOrDefault();
                    
    return result;
}
```

### Method B: The Senior Answer (Min-Heap / Priority Queue)

If the array has 10 million rows and you want the 3rd largest, sorting 10 million rows is a waste of CPU. Instead, you use a **Priority Queue** (Min-Heap) to maintain a running "Top 3" list. This drops the time complexity to $O(N \log K)$.

**How it works:**

1. Create a Priority Queue that keeps the _smallest_ number at the front of the line.
    
2. Throw numbers into the queue.
    
3. If the queue gets larger than $K$ (e.g., larger than 3), immediately dequeue (kick out) the smallest number.
    
4. When the loop finishes, the queue contains exactly the 3 largest numbers. Because it's a Min-Heap, the 3rd largest (the smallest of the top 3) is sitting right at the front.
    

C#

```cs
using System.Collections.Generic;

public static int FindKthLargestHeap(int[] arr, int k)
{
    // C# 10 introduced PriorityQueue
    // The first int is the element, the second int is the Priority
    var minHeap = new PriorityQueue<int, int>();

    // Note: To handle duplicates like the previous examples, 
    // you would pass arr.Distinct() into this loop instead.
    foreach (int number in arr)
    {
        // Enqueue the number, using the number itself as its priority
        minHeap.Enqueue(number, number);

        // If our "Top K" list exceeds K, kick out the lowest priority (smallest) number
        if (minHeap.Count > k)
        {
            minHeap.Dequeue();
        }
    }

    // The element at the front of the queue is the K-th largest
    return minHeap.Peek();
}
```

|**Metric**|**3-Variable Tracking**|**LINQ Sorting**|**Min-Heap (Priority Queue)**|
|---|---|---|---|
|**Time Complexity**|$O(N)$|$O(N \log N)$|$O(N \log K)$|
|**Space Complexity**|$O(1)$|$O(N)$|$O(K)$|
|**Scalability**|Terrible ($K=3$ max)|Poor (Slows down on massive arrays)|Excellent (Industry standard for $K$-th largest)|

**Pro-Tip:** ⚠️ If you use the Priority Queue approach in an interview, be sure to ask the interviewer if they want the $K$-th largest _distinct_ element or just the $K$-th largest overall. If they want distinct, you must run a `HashSet` or `.Distinct()` filter over the array before feeding it into the heap.