This is another **very common .NET interview question**. Interviewers usually ask it like this:

* What is Garbage Collection?
* How does the Garbage Collector work?
* When does it run?
* Can we force it?
* What are the GC generations?

Let's build it from first principles.

---

# What is Garbage Collection?

Imagine you rented a hotel room.

When you leave, housekeeping cleans the room.

You don't have to clean it yourself.

The **Garbage Collector (GC)** is the housekeeping service for memory.

Its job is to:

> **Automatically find objects that are no longer being used and free their memory.**

Without GC, you'd have to manually free memory like in C/C++.

---

# Example

```csharp
public class Employee
{
    public string Name { get; set; }
}

void Test()
{
    Employee emp = new Employee();

    emp.Name = "John";
}
```

Memory

```
Stack                  Heap

emp -------------> Employee
                     Name = John
```

When `Test()` ends

```
Stack

(empty)
```

Nothing points to the Employee object anymore.

The object becomes

```
Unreachable
```

Eventually,

```
Garbage Collector

↓

Deletes Employee object

↓

Memory becomes available again
```

---

# Important Interview Point

The GC **does not** immediately delete the object.

It waits until it decides it's a good time.

This improves performance.

---

# How does GC know an object is garbage?

The GC starts from **roots**.

GC Roots include

* Local variables on the stack
* Static variables
* CPU registers
* Objects referenced by other live objects

Example

```
Stack

emp -------> Employee

             ↓
          Address
```

Employee is reachable.

Now

```csharp
emp = null;
```

```
Stack

emp = null

Heap

Employee
```

No references exist.

The object is now eligible for collection.

---

# When does GC run?

This is one of the most asked questions.

The answer is

> **You don't know exactly.**

The CLR decides.

Usually when

* Heap memory becomes low
* Many objects have been allocated
* The application is idle (sometimes)
* `GC.Collect()` is called (generally discouraged)

---

Example

```csharp
for(int i=0;i<1000000;i++)
{
    new Employee();
}
```

Lots of memory allocated.

Eventually

```
Heap almost full

↓

CLR triggers GC

↓

Unused objects removed

↓

Continue execution
```

---

# Can we call it ourselves?

Yes.

```csharp
GC.Collect();
```

But interview answer:

> **Avoid calling it manually unless you have a very specific reason.**

Why?

The CLR knows better than you when collection is worthwhile.

Forcing GC too often can actually reduce performance.

---

# How does GC work?

The basic process is:

### Step 1

Stop the application briefly.

```
Application paused
```

This is called a **Stop-the-World** pause.

---

### Step 2

Find all reachable objects.

```
Stack

↓

Object A

↓

Object B

↓

Object C
```

These survive.

---

### Step 3

Find unreachable objects.

```
Object D

Object E

Object F
```

No references.

Delete them.

---

### Step 4

Compact memory.

```
Before

A
(empty)
B
(empty)
C
```

↓

```
After

A
B
C
```

This reduces fragmentation.

---

# Generational GC

This is almost guaranteed in interviews.

The CLR assumes:

> Most objects die young.

Example

```csharp
string temp = "abc";
```

Used once.

Gone.

No reason to keep checking it forever.

---

There are three generations.

## Generation 0

New objects.

```
new Employee()

↓

Gen 0
```

Most objects die here.

GC checks this most frequently.

---

## Generation 1

Objects that survived Gen 0.

```
Gen0 survives

↓

Gen1
```

---

## Generation 2

Long-lived objects.

```
Configuration

Singleton

Large caches
```

They survive multiple collections.

---

Interview table

| Generation | Meaning            |
| ---------- | ------------------ |
| Gen 0      | New objects        |
| Gen 1      | Medium lifetime    |
| Gen 2      | Long-lived objects |

---

# Large Object Heap (LOH)

Objects larger than roughly **85 KB** go to the Large Object Heap.

Example

```csharp
byte[] data = new byte[100000];
```

This bypasses the small object generations and is managed separately.

---

# IDisposable vs Garbage Collector

This question appears frequently.

Suppose

```csharp
FileStream fs = new FileStream(...);
```

The GC will eventually free the `FileStream` object.

But the file handle is an unmanaged OS resource.

So we use

```csharp
using var fs = new FileStream(...);
```

or

```csharp
fs.Dispose();
```

GC frees **managed memory**.

`Dispose()` releases **unmanaged resources** promptly.

---

# Finalizer

```csharp
class Test
{
    ~Test()
    {
        Console.WriteLine("Cleaning");
    }
}
```

Runs before GC reclaims the object.

Interview point:

Finalizers make collection more expensive.

Avoid them unless you're wrapping unmanaged resources.

---

# Weak Reference

Advanced interview topic.

Normally

```csharp
Employee emp = new Employee();
```

The object stays alive because `emp` references it.

With

```csharp
WeakReference<Employee>
```

the GC is still allowed to collect the object if needed.

Useful for caches.

---

# Common Interview Questions

## Q1. Does setting an object to null immediately free memory?

```csharp
emp = null;
```

❌ No.

It only removes that reference.

The object becomes **eligible** for collection if nothing else references it.

---

## Q2. Can GC collect an object still in use?

No.

If an object is reachable from a GC root, it won't be collected.

---

## Q3. Can GC collect static objects?

Generally no, while they're still referenced by static fields.

Static objects usually live until the application (or AppDomain) ends or the static reference is cleared.

---

## Q4. Does `Dispose()` call GC?

No.

It releases resources.

GC still decides when to reclaim the managed object.

---

## Q5. What is a memory leak in C#?

Many people think C# can't leak memory.

It can.

Example

```csharp
static List<Employee> cache = new();
```

```csharp
cache.Add(new Employee());
```

If you keep adding forever,

the objects remain reachable through the static list.

GC cannot collect them.

This is a **managed memory leak**.

---

# Interview Answer (1–2 minutes)

> **The Garbage Collector (GC) is an automatic memory management system in .NET. It identifies objects that are no longer reachable from GC roots, such as local variables, static fields, and active references, and reclaims their memory. The CLR decides when to run the GC based on factors like memory pressure and allocation patterns. The .NET GC is generational, organizing objects into Generation 0, 1, and 2 because most objects have short lifetimes. It also compacts memory to reduce fragmentation. Developers generally should not call `GC.Collect()` manually, as the runtime is optimized to determine the best time for collection. It's also important to distinguish GC from `IDisposable`: the GC reclaims managed memory, while `Dispose()` is used to release unmanaged resources like file handles or database connections promptly.**
