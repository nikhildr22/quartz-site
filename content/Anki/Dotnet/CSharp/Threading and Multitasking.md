STARTanki
Basic

What is a process?

Back:
A process is an independent running program with its own memory space.

Examples:
- Chrome
- Visual Studio
- SQL Server
<!--ID: 1783396917426-->
ENDanki

STARTanki
Basic

What is a thread?

Back:
A thread is the smallest unit of execution inside a process.

Multiple threads within the same process share memory.
<!--ID: 1783396917428-->
ENDanki

STARTanki
Basic

What is multithreading?

Back:
Multithreading is executing multiple threads concurrently within a single process.

Example:
An ASP.NET Core application handling multiple HTTP requests simultaneously.
<!--ID: 1783396917429-->
ENDanki

STARTanki
Basic

Why do we use multithreading?

Back:
Reasons:
- Improve responsiveness
- Better CPU utilization
- Perform background work
- Execute multiple tasks concurrently
<!--ID: 1783396917431-->
ENDanki

STARTanki
Basic

Why is Task preferred over Thread?

Back:
Task:
- Uses the ThreadPool
- Less overhead
- Easier error handling
- Supports async/await
- Supports cancellation

Thread creates a dedicated OS thread.
<!--ID: 1783396917432-->
ENDanki

STARTanki
Basic

What is the ThreadPool?

Back:
ThreadPool is a pool of reusable worker threads managed by .NET.

Benefits:
- Reduces thread creation cost
- Improves performance
- Used internally by Task and ASP.NET Core
<!--ID: 1783396917434-->
ENDanki

STARTanki
Basic

Does async/await create a new thread?

Back:
No.

`async/await` enables non-blocking asynchronous programming.
It does **not** create a new thread by itself.
<!--ID: 1783396917436-->
ENDanki

STARTanki
Basic

What is the difference between CPU-bound and I/O-bound work?

Back:
CPU-bound:
- Heavy computation
- Use `Task.Run()` or `Parallel`

I/O-bound:
- Database
- HTTP
- File I/O
- Use async methods like `ToListAsync()`
<!--ID: 1783396917438-->
ENDanki

STARTanki
Basic

When should you use Task.Run()?

Back:
Use `Task.Run()` for CPU-bound work.

```csharp
await Task.Run(() => Calculate());
```

Do **not** wrap naturally asynchronous I/O operations in `Task.Run()`.
<!--ID: 1783396917439-->
ENDanki

STARTanki
Basic

What is Task.WhenAll() used for?

Back:
Runs multiple asynchronous tasks concurrently and waits until all complete.

```csharp
await Task.WhenAll(
    GetUsers(),
    GetOrders(),
    GetProducts());
```
<!--ID: 1783396917441-->
ENDanki

STARTanki
Basic

What is Task.WhenAny() used for?

Back:
Returns when the first task completes.

```csharp
Task first = await Task.WhenAny(task1, task2);
```
<!--ID: 1783396917443-->
ENDanki

STARTanki
Basic

What is a race condition?

Back:
A race condition occurs when multiple threads access shared data simultaneously, leading to unpredictable results.

Use `lock` or `Interlocked` to prevent it.
<!--ID: 1783396917444-->
ENDanki

STARTanki
Basic

What is the purpose of the lock statement?

Back:
`lock` ensures only one thread accesses a critical section at a time.

```csharp
private readonly object _lock = new();

lock (_lock)
{
    counter++;
}
```
<!--ID: 1783396917446-->
ENDanki

STARTanki
Basic

What is Interlocked.Increment()?

Back:
Performs an atomic increment without using a lock.

```csharp
Interlocked.Increment(ref counter);
```

Useful for simple thread-safe counters.
<!--ID: 1783396917448-->
ENDanki

STARTanki
Basic

What is a deadlock?

Back:
A deadlock occurs when two or more threads wait indefinitely for each other to release resources.

Avoid nested locks and inconsistent lock ordering.
<!--ID: 1783396917450-->
ENDanki

STARTanki
Basic

What is CancellationToken used for?

Back:
Allows an operation to be cancelled gracefully.

```csharp
await DoWork(token);

token.ThrowIfCancellationRequested();
```
<!--ID: 1783396917451-->
ENDanki

STARTanki
Basic

What is SemaphoreSlim used for?

Back:
Limits the number of threads that can access a resource concurrently.

```csharp
SemaphoreSlim semaphore = new(3);

await semaphore.WaitAsync();

try
{
    // work
}
finally
{
    semaphore.Release();
}
```
<!--ID: 1783396917454-->
ENDanki

STARTanki
Basic

What is the difference between Thread and Task?

Back:
**Thread**
- Low-level
- Dedicated OS thread
- Higher overhead

**Task**
- High-level abstraction
- Uses ThreadPool
- Supports async/await
- Preferred in modern .NET
<!--ID: 1783396917455-->
ENDanki

STARTanki
Basic

Explain async/await.

Back:
`async/await` simplifies asynchronous programming by allowing a method to pause without blocking a thread while waiting for an asynchronous operation to complete.

It is primarily used for I/O-bound operations and improves application scalability.
<!--ID: 1783396917457-->
ENDanki

STARTanki
Basic

What is the output of this code?

Back:

```csharp
Console.WriteLine("1");

await Task.Delay(1000);

Console.WriteLine("2");
```

Output:

```
1
(after 1 second)
2
```

Execution pauses at `await` and resumes after the awaited task completes.
<!--ID: 1783396917459-->
ENDanki

STARTanki
Basic

What is the output of this code?

Back:

```csharp
Console.WriteLine("1");

Task.Delay(1000);

Console.WriteLine("2");
```

Output:

```
1
2
```

`Task.Delay()` creates a Task but it is never awaited, so execution continues immediately.

ENDanki

STARTanki
Basic

What is the output of this code?

Back:

```csharp
Console.WriteLine("1");

var task = Task.Delay(1000);

Console.WriteLine("2");

await task;

Console.WriteLine("3");
```

Output:

```
1
2
(after 1 second)
3
```

The delay starts immediately, but execution continues until `await task`.

ENDanki

STARTanki
Basic

What is the output of this code?

Back:

```csharp
for(int i = 1; i <= 3; i++)
{
    Console.WriteLine(i);
    await Task.Delay(1000);
}
```

Output:

```
1
(wait)
2
(wait)
3
```

Each iteration waits before continuing to the next.

ENDanki

STARTanki
Basic

What is the output of this code?

Back:

```csharp
for(int i = 1; i <= 3; i++)
{
    Task.Delay(1000);
    Console.WriteLine(i);
}
```

Output:

```
1
2
3
```

All delays are ignored because they are never awaited.

ENDanki

STARTanki
Basic

What is the output of this code?

Back:

```csharp
Console.WriteLine("A");

Task task = Task.Run(() =>
{
    Console.WriteLine("B");
});

Console.WriteLine("C");

await task;
```

Possible output:

```
A
C
B
```

or

```
A
B
C
```

`Task.Run()` executes on another thread, so the order of `B` and `C` is not guaranteed.

ENDanki

STARTanki
Basic

What is the output of this code?

Back:

```csharp
Console.WriteLine("Start");

await Task.Run(() =>
{
    Console.WriteLine("Working");
});

Console.WriteLine("End");
```

Output:

```
Start
Working
End
```

The final line executes only after the background task completes.

ENDanki

STARTanki
Basic

What is the output of this code?

Back:

```csharp
var t1 = Task.Delay(1000);
var t2 = Task.Delay(1000);

await Task.WhenAll(t1, t2);

Console.WriteLine("Done");
```

Output:

```
(after ~1 second)
Done
```

Both tasks run concurrently.

ENDanki

STARTanki
Basic

What is the output of this code?

Back:

```csharp
await Task.Delay(1000);
await Task.Delay(1000);

Console.WriteLine("Done");
```

Output:

```
(after ~2 seconds)
Done
```

The delays execute sequentially.

ENDanki

STARTanki
Basic

What is the difference between these two snippets?

Back:

Concurrent:

```csharp
Task t1 = GetUsers();
Task t2 = GetOrders();

await Task.WhenAll(t1, t2);
```

Sequential:

```csharp
await GetUsers();
await GetOrders();
```

The first runs both operations simultaneously.
The second waits for the first to finish before starting the second.
<!--ID: 1783396917468-->
ENDanki

STARTanki
Basic

What is wrong with this code?

Back:

```csharp
await Task.Run(async () =>
{
    await SaveAsync();
});
```

Usually unnecessary.

If `SaveAsync()` is already asynchronous (I/O-bound), simply do:

```csharp
await SaveAsync();
```

Avoid wrapping async I/O methods inside `Task.Run()`.
<!--ID: 1783396917471-->
ENDanki

STARTanki
Basic

Should you use Task.Run() for Entity Framework or HttpClient?

Back:
No.

These APIs are already asynchronous.

✔ Correct

```csharp
await db.Users.ToListAsync();

await httpClient.GetAsync(url);
```

❌ Avoid

```csharp
await Task.Run(() =>
    db.Users.ToListAsync());
```
<!--ID: 1783396917473-->
ENDanki

STARTanki
Basic

When should you use Task.Run()?

Back:
Only for CPU-bound work.

Examples:
- Image processing
- Compression
- Encryption
- Large calculations

Do not use it for:
- Database calls
- HTTP requests
- File I/O

ENDanki

STARTanki
Basic

What is the difference between Task.Run() and async/await?

Back:

`Task.Run()`
- Starts work on a ThreadPool thread.
- Used for CPU-bound work.

`async/await`
- Does not create a thread.
- Makes asynchronous I/O non-blocking.
<!--ID: 1783396917477-->
ENDanki

STARTanki
Basic

Why is async/await good for ASP.NET Core?

Back:
While an async operation (database, HTTP, file I/O) is waiting, the request thread is returned to the ThreadPool.

This allows ASP.NET Core to serve more requests with fewer threads, improving scalability.
<!--ID: 1783396917479-->
ENDanki