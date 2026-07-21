
---
Created: 24th December 2022 05:35 AM
alias: [c#, .net, dotnet interview, questpond]
Status: 
Medium: 
Tags: [inbox, dotnet, ankied ]
url: https://youtu.be/BKynEBPqiIM
links: 
---




STARTanki
Basic
# Explain difference between .NET and C# ?
Back:


one is framework, one is a programming language.
framework has a collection of libraries.
framework has CLR that can run our applications.

we use both to create applications.
What does the interviewer want to hear
.NET is a framework and C# is a programming language
<!--ID: 1672269699072-->
ENDanki

STARTanki
Basic
# Differentiate between .NET framework vs .NET Core vs .NET 5.0
Back:

Pick 3 most important differences.

![[Pasted image 20221224053842.png]]
performance improvements:
![[Pasted image 20221224054025.png]]

CLI tools:
![[Pasted image 20221224054055.png]]
with this we can use any IDE.

![[Pasted image 20221224053829.png]]


![[Pasted image 20221224054139.png]]
<!--ID: 1672269699085-->
ENDanki

STARTanki
Basic
# What is IL ( Intermediate Language) Code ?
Back:

What does the interviewer want to hear
==IL Code is a partially compiled code.==
JIT compiles IL code to Machine language.
![[Pasted image 20221224054229.png]]
<!--ID: 1672269699089-->
ENDanki

STARTanki
Basic
# What is the use of JIT ( Just in time compiler) ?
Back:

What does the interviewer want to hear
IL Code is a partially compiled code.
JIT compiled IL code to Machine language.
![[Pasted image 20221224054229.png]]
<!--ID: 1672269699093-->
ENDanki

STARTanki
Basic
# Is it possible to view IL code ?
Back:

![[Pasted image 20221224054334.png]]
we can see the DLL contents using tools like  [ILDASM](http://msdn.microsoft.com/en-us/library/f7dy01k1(v=vs.80).aspx)

![[Pasted image 20221224054522.png]]
<!--ID: 1672269699097-->
ENDanki

STARTanki
Basic
# What is the benefit of compiling in to IL code ?
Back:


because dev and runtime environment can be different.


What does the interviewer want to hear ?
The runtime environment and development environment can be very
different. So depending on the runtime environment JIT compiles IL the best optimized code as per that environment.
<!--ID: 1672269699101-->
ENDanki

STARTanki
Basic
# Does .NET support multiple programming languages ?
Back:


yes. But the end, all the code will be compiled into IL code.
<!--ID: 1672269699106-->
ENDanki

STARTanki
Basic
# What is CLR ( Common Language Runtime) ?
Back:

- converts IL to native language
- helps to execute ,net app
- runs garbage collector

What does the interviewer want to hear ?
- -- CLR invokes JIT to compile IL code to native code
- -- Cleans any unused objects by using Garbage Collector.



![[Pasted image 20221224055030.png]]
<!--ID: 1672269699111-->
ENDanki

STARTanki
Basic
# What is managed and unmanaged code ?
Back:

code that runs under the umbrella of CLR is Managed code.

What does the interviewer want to hear ?
Code that executes under CLR execution environment is called as managed code.
Unmanaged code executes outside CLR boundary. Unmanaged code is nothing but code written in C++ , VB6 , VC++ etc.
Unmanaged codes have their own environment in which the code runs and it's completely outside the control of CLR.
<!--ID: 1672269699115-->
ENDanki

STARTanki
Basic
# Explain the importance of Garbage collector ?
Back:


background process, cleans any kind of ==unused **managed**== resources


What does the interviewer want to hear ?
Garbage Collector is a back ground process which cleans unused
Managed resources.
<!--ID: 1672269699120-->
ENDanki

STARTanki
Basic
# Can garbage collector claim unmanaged objects ?
Back:

NO
<!--ID: 1672269699124-->
ENDanki

STARTanki
Basic
# What is the importance of CTS ?
Back:

What does the interviewer want to hear ?
CTS (Common types system) ensures that data types defined in
two different languages gets compiled to a common data type.
![[Pasted image 20221224055441.png]]
<!--ID: 1672269699129-->
ENDanki

STARTanki
Basic
# Explain CLS ?
Back:

![[Pasted image 20221224055540.png]]
common language specification.
set of guidlines.
What does the interviewer want to hear ?
CLS is a specification or set of rules or guidelines. When any .NET
programming language adheres to these set of rules it can be
consumed by any language following .NET specifications.
<!--ID: 1672269699134-->
ENDanki

STARTanki
Basic
# Difference between Stack vs Heap ?
Back:

in stack, variable and data both are stored in same place.
What does the interviewer want to hear ?
Stack and heap are memory types in an application. Stack memory stores data types
like int , double , Boolean etc. While heap stores data types like string and objects.
![[Pasted image 20221224055717.png]]
<!--ID: 1672269699138-->
ENDanki

STARTanki
Basic
# What are Value types & Reference types?
Back:

What does the interviewer want to hear ?
Value types contain actual data while reference types contain pointers
and the pointers point to the actual data.
Value types are stored on stack while reference types are stored on heap.
Value types are your normal data types like int , bool , double and reference types are all objects.
<!--ID: 1672269699142-->
ENDanki

STARTanki
Basic
# What is boxing and unboxing?
Back:



What does the interviewer want to hear ?
When value type is moved to a reference type it's called as boxing. The vice-
versa is termed as unboxing
![[Pasted image 20221224063010.png]]
<!--ID: 1672269699147-->
ENDanki

STARTanki
Basic
# What is consequence of boxing and unboxing ?
Back:

performance impact, as we are moving data from stack to heap or vice versa.
![[Pasted image 20221224063010.png]]
<!--ID: 1672269699151-->
ENDanki

STARTanki
Basic
# Explain casting,implicit casting and explicit casting?
Back:

![[Pasted image 20221224063152.png]]
when you are moving from lower datatype to higher datatype, the conversion happens implicitly.
but while moving from from higher datatype to lower datatype .

What does the interviewer want to hear ?
Type casting is a mechanism where we convert one type of data to other type.
Implicit casting is when you move from lower to higher data type.
l.
Explicit casting is when you move from higher to lower datatype.

==Explicit takes extra attention from developer, because we need to make sure there's no data loss during conversion from higher datatype to lower datatype==
<!--ID: 1672269699156-->
ENDanki

STARTanki
Basic
# What can happen during explicit casting ?
Back:

there'll be a possibility data loss.
What does the interviewer want to hear ?
In explicit casting you can have data loss.
<!--ID: 1672269699161-->
ENDanki

STARTanki
Basic
# Array VS ArrayList ?
Back:


![[Pasted image 20221224063555.png]]
<!--ID: 1672269699165-->
ENDanki

STARTanki
Basic
# Whose performance is better array or arraylist ?
Back:

What does the interviewer want to hear ?
ArrayList is slower than Array because of
Boxing and Unboxing.
<!--ID: 1672269699170-->
ENDanki

STARTanki
Basic
# What are generic collections ?
Back:

What does the interviewer want to hear ?
Generic collection is strongly typed and flexible. It has better performance as compared to ArrayList.

![[Pasted image 20221224063649.png]]
![[Pasted image 20221229042601.png]]
<!--ID: 1672269699175-->
ENDanki

STARTanki
Basic
# What are threads (Multithreading)?
Back:

What does the interviewer want to hear ?
If we want to run code parallely then we use threads.
![[Pasted image 20221224063801.png]]
<!--ID: 1672269699180-->
ENDanki

STARTanki
Basic
# How are threads different from TPL ? difference between thread and task.
Back:



![[Pasted image 20221224063953.png]]
![[Pasted image 20221224064012.png]]


In latest .net versions its better to use Tasks/TPL as the can run parallely.
<!--ID: 1672269699185-->
ENDanki

STARTanki
Basic
# use of `finally` block?
Back:

it'll always run.
<!--ID: 1672269699190-->
ENDanki

STARTanki
Basic
# Why do we need the `out` keyword ?
Back:

What does the interviewer want to hear ?
If you want to return multiple outputs from a function you will use OUT keyword.
![[Pasted image 20221224064438.png]]
<!--ID: 1672269699194-->
ENDanki

STARTanki
Basic
# What is the need of Delegates ?
Back:

Delegate is a pointer to a function and very useful as callbacks to communicate between threads.
<!--ID: 1672269699199-->
ENDanki

STARTanki
Basic
# What are events ?
Back:

Events are encapsulation over delegates.
<!--ID: 1672269699204-->
ENDanki

STARTanki
Basic
# Whats the difference between Abstract class and interface ?
Back:

Abstract class is a half defined parent class while interface  is a contract.
Abstract class is inherited while interface is implemented .
<!--ID: 1672269699209-->
ENDanki

