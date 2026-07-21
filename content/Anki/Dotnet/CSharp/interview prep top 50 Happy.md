---
alias: []
Status:
Medium:
Tags:
  - dotnet
  - ankied
url: https://www.youtube.com/watch?v=Bai9_LSZfAI
links:
  - - interview prep top 50 Happy
---


# interview prep top 50 Happy




STARTanki
Basic
# what are main concepts of OOPs? or 4 pillars of OOPs. APIE
Back:


![[Pasted image 20221218050012.png]]
![[Pasted image 20221219061438.png]]
<!--ID: 1671497277414-->
ENDanki

STARTanki
Basic
# whats a class, object, variable,constructor, method
Back:

![[Pasted image 20221218050202.png]]
<!--ID: 1671497277428-->
ENDanki

STARTanki
Basic
# what is inheritence and why its important?
Back:
nheritance is creating a PARENT-CHILD relationship
etween two classes where child class will
utomatically get the properties and methods of the
arent.

Inheritance is good for: REUSABILITY and
ABSTRACTION of code
![[Pasted image 20221218050418.png]]
<!--ID: 1671497277440-->
ENDanki

STARTanki
Basic
# how to prevent a class from being inherited?
Back:

use sealed keyword
![[Pasted image 20221218050449.png]]
or static class (but in this case all methods and fields should be made static too)
![[Pasted image 20221218050518.png]]

==why do we even have to do that?==

🚀 Key Benefits

- **Security**: Prevents unauthorized modifications or overrides of sensitive logic (e.g., `System.String` is sealed).
- **Speed**: Enables **JIT devirtualization** and method inlining, removing performance lookup penalties.
- **API Design**: Signals a complete, standalone component designed for **composition** instead of inheritance.
- **Maintenance**: Avoids breaking downstream code since removing `sealed` later is completely safe.
<!--ID: 1671497277451-->
ENDanki

STARTanki
Basic
# whats is abstraction
Back:
Abstraction means showing only required things and hide the **BACKGROUND** details.
![[Pasted image 20221218050621.png]]
>the abstracted methods can have any access modifier depENDankiing on the use case.
<!--ID: 1671497277461-->
ENDanki

STARTanki
Basic
# 4 types of inhertence?
Back:

1. single
2. multiple (using interfaces)
3. multilevel
4. heirarchical

![[Pasted image 20221218050835.png]]
<!--ID: 1671497277474-->
ENDanki

STARTanki
Basic
# method polymorphism and its 2 types? (its different than object polymorphism )
Back:
Polymorphism is the ability of a variable, object, or function to take on MULTIPLE FORMS.
2 types:
1. compile time
2. run time
![[Pasted image 20221218050932.png]]
<!--ID: 1671497277485-->
ENDanki

STARTanki
Basic
# Encapsulation , how to violate encapsulation ?
Back:
==Encapsulation means **WRAPPING** of data and methods/properties into a single unit.==
using access modifiers to  decide we can decide what to hide and only those can be accessed using properties.
![[Pasted image 20221218051133.png]]
<!--ID: 1671497277496-->
ENDanki

STARTanki
Basic
# What is Method Overloading? In how many ways a method can be overloaded?
Back:


3 ways we can overload:

![[Pasted image 20221218051249.png]]
<!--ID: 1671497277507-->
ENDanki

STARTanki
Basic
# difference between overloading and overriding?
Back:

overriding we do in an inherited class

![[Pasted image 20221218051430.png]]
<!--ID: 1671497277518-->
ENDanki

STARTanki
Basic
# What is the difference between Method Overriding and Method Hiding ?
Back:

![[Pasted image 20221218051544.png]]
<!--ID: 1671497277528-->
ENDanki

STARTanki
Basic
# What are the advantages and limitations of OOPS ?
Back:
## Advantages:
1. Reuse of code through inheritance
2. Flexibility through polymorphism
3. Security of data through Data hiding/ Encapsulation.
4. Simple to upgrade/ scale from smaller to larger applications.
5. Modularity for easier troubleshooting.
## Disadvantage of OOPS:
It is not suitable for small applications.
<!--ID: 1671497277538-->
ENDanki

STARTanki
Basic
# What is the difference between an Abstract class and an Interface (atleast 4)?
Back:


![[Pasted image 20221218051804.png]]


> it does not support multiple inheritence ,  thats why we need interface.
<!--ID: 1671497277553-->
ENDanki

STARTanki
Basic
# When to use Interface and when Abstract class?
Back:


![[Pasted image 20221218052013.png]]
<!--ID: 1671497277564-->
ENDanki

STARTanki
Basic
# Why to even create Interfaces ?
Back:


- to maintain consistency across all inherited classes
- it allows multiple inheritence

![[Pasted image 20221218052231.png]]
<!--ID: 1671497277576-->
ENDanki

STARTanki
Basic
# Do Interface can have a Constructor?
Back:


==nope==
<!--ID: 1671497277586-->
ENDanki

STARTanki
Basic
# Can you create an instance of an Abstract class or an Interface ?
Back:


==Nope==
#todo 
- [ ] then why we need a constructor  in abstract class when its never going to have an object.

sole purpose of inheritence 
<!--ID: 1671497277597-->
ENDanki

STARTanki
Basic
# What are Access Specifiers? What is the default access modifier in a class?
Back:

we can use these to achieve encapsulation .
![[Pasted image 20221218052745.png]]
<!--ID: 1671497277608-->
ENDanki

STARTanki
Basic
# What is Boxing and Unboxing ?
Back:

unboxing is explicit conversion.
![[Pasted image 20221218052855.png]]
<!--ID: 1671497277619-->
ENDanki

STARTanki
Basic
# What is the difference between “String” and “StringBuilder”? When to use what?
Back:
string is **IMMUTABLE** in c#, StringBuilder is **MUTABLE**

![[Pasted image 20221218053003.png]]
<!--ID: 1671497277630-->
ENDanki

STARTanki
Basic
# What are the 4 basic string operations in C# ? (CCRT)
Back:


![[Pasted image 20221218053843.png]]
<!--ID: 1671497277642-->
ENDanki

STARTanki
Basic
# What are Nullable types ?
Back:

![[Pasted image 20221219051639.png]]
![[Pasted image 20221219051649.png]]
valid way:
![[Pasted image 20221219051721.png]]
<!--ID: 1671497277656-->
ENDanki

STARTanki
Basic
# How to implement Exception Handling in C# ? 4 keywords used in exception handling.
Back:


- try
- catch
- throw
- finally

![[Pasted image 20221219051835.png]]
<!--ID: 1671497277667-->
ENDanki

STARTanki
Basic
# Explain Generics in C# ? When and why to use them ?
Back:


![[Pasted image 20221219051958.png]]
one way: making the method generic
![[Pasted image 20221219052034.png]]
another way: making the class generic
![[Pasted image 20221219052049.png]]
<!--ID: 1671497277680-->
ENDanki

STARTanki
Basic
# Can we execute multiple Catch blocks ?
Back:


No, only one of them will be executed
![[Pasted image 20221219052139.png]]
<!--ID: 1671497277693-->
ENDanki

STARTanki
Basic
# What is a Finally block and give an example when to use it ?
Back:


![[Pasted image 20221219052219.png]]
<!--ID: 1671497277706-->
ENDanki

STARTanki
Basic
# Can we have only “Try” block without “Catch” block ?
Back:


![[Pasted image 20221219052257.png]]
<!--ID: 1671497277718-->
ENDanki

STARTanki
Basic
# What is the difference between “throw ex” and “throw”?
Back:


![[Pasted image 20221219052441.png]]
![[Pasted image 20221219052640.png]]
<!--ID: 1671497277730-->
ENDanki

STARTanki
Basic
# What are the 4 Loop types in C#?
Back:

while 
do while
for 
foreach

![[Pasted image 20221219052738.png]]
![[Pasted image 20221219052812.png]]
<!--ID: 1671497277742-->
ENDanki

STARTanki
Basic
# What is the difference between “continue” and “break” statement?
Back:


![[Pasted image 20221219052910.png]]
<!--ID: 1671497277751-->
ENDanki

STARTanki
Basic
# What is the difference between Array and ArrayList (atleast 2)?
Back:


![[Pasted image 20221219053037.png]]
<!--ID: 1671497277762-->
ENDanki

STARTanki
Basic
# What is the difference between Arraylist and Hashtable?
Back:


![[Pasted image 20221219053118.png]]
<!--ID: 1671497277772-->
ENDanki

STARTanki
Basic
# What are Collections in C# and what are their types(3 types)?
Back:


![[Pasted image 20221219053224.png]]
concurrent collections can be used during multithreading
<!--ID: 1671497277782-->
ENDanki

STARTanki
Basic
# What is IEnumerable in C#?
Back:


IEnumerable helps in iteration of a collection.

![[Pasted image 20221219053441.png]]
Internally the list is using IEnumerable interface for foreach loop

![[Pasted image 20221219053504.png]]
<!--ID: 1671497277792-->
ENDanki

STARTanki
Basic
# What is the difference between IEnumerable and IEnumerator in C# ?
Back:


![[Pasted image 20221219053619.png]]
![[Pasted image 20221219053624.png]]
<!--ID: 1671497277802-->
ENDanki

STARTanki
Basic
# What is the difference between IEnumerable and IQueryable in C#?
Back:

we can use IQueryable to reduce the network load.

![[Pasted image 20221219053726.png]]
<!--ID: 1671497277811-->
ENDanki

STARTanki
Basic
# What is the difference between “out” and “ref” parameters?
Back:
Both indicate that an argument/parameter is **passed by reference**. 
By default parameters are passed to a method by value. but By using these keywords (ref and out) we can pass a parameter by reference.
passing arguments by reference means any changes made to this argument in the method will be reflected in that variable when control returns to the calling method.
==ref needs initialization, but out does not (it sounds logical as the compiler knows that the output parameter dont need to be initialized before getting the output)==


![[Pasted image 20221219053934.png]]
<!--ID: 1671497277821-->
ENDanki

STARTanki
Basic
# What is the purpose of “params” keyword ?
Back:


![[Pasted image 20221219054114.png]]
<!--ID: 1671497277831-->
ENDanki

STARTanki
Basic
# What is a Constructor and what are its 5 types ?
Back:

5 types
1. Default constructor
2. Parameterized constructor
3. Copy constructor
4. Static constructor
5. Private constructor
![[Pasted image 20221219054300.png]]
![[Pasted image 20221219054322.png]]

![[Pasted image 20221219054405.png]]
![[Pasted image 20221219054415.png]]

![[Pasted image 20221219054506.png]]
whats the use if it cant be used or inherited?
its used in singleton design pattern.

![[Pasted image 20221219054612.png]]
it'll copy.
<!--ID: 1671497277841-->
ENDanki

STARTanki
Basic
# When to use Private constructor?
Back:

![[Pasted image 20221219054704.png]]
<!--ID: 1671497277851-->
ENDanki

STARTanki
Basic
# What are Extension Methods in C#? When to use them?
Back:


![[Pasted image 20221219054807.png]]
it should be staic class, it should be static method
we need to use `this` keyword.
<!--ID: 1671497277862-->
ENDanki

STARTanki
Basic
# What are Anonymous Delegates in C#?
Back:


![[Pasted image 20221219054946.png]]
inline methods
<!--ID: 1671497277871-->
ENDanki

STARTanki
Basic
# What are the differences between Events and Delegates?
Back:


![[Pasted image 20221219055058.png]]
#rewatch 
<!--ID: 1671497277884-->
ENDanki

STARTanki
Basic
# What is “this” keyword in C# ? When to use it ?
Back:


![[Pasted image 20221219055219.png]]
<!--ID: 1671497277896-->
ENDanki

STARTanki
Basic
# What are Multicast Delegates ?
Back:


![[Pasted image 20221219055415.png]]
it'll call multiple methods.
<!--ID: 1671497277909-->
ENDanki

STARTanki
Basic
# What you mean by Delegate? When to use them?
Back:


![[Pasted image 20221219055558.png]]
![[Pasted image 20221219055729.png]]
#doubt where do we use delegates in real life.
<!--ID: 1671497277921-->
ENDanki

STARTanki
Basic
# What is “Static” class? When to use it?
Back:


![[Pasted image 20221219055849.png]]
<!--ID: 1671497277931-->
ENDanki

STARTanki
Basic
# What is the purpose of “using” keyword in C#?
Back:


![[Pasted image 20221219060018.png]]
if we dont dispose, it'll impact performance.

![[Pasted image 20221219060041.png]]
it'll work only on those classes which implement IDisposable interface.
<!--ID: 1671497277941-->
ENDanki

STARTanki
Basic
# What is the difference between “is” and “as” operators?
Back:


![[Pasted image 20221219060215.png]]
<!--ID: 1671497277951-->
ENDanki

STARTanki
Basic
# What is the difference between “var” and “dynamic” in C#?
Back:


![[Pasted image 20221219060312.png]]
<!--ID: 1671497277960-->
ENDanki

STARTanki
Basic
# What is the difference between “Readonly” and “Constant” variables (atleast 3)?
Back:


![[Pasted image 20221219060500.png]]
<!--ID: 1671497277969-->
ENDanki

STARTanki
Basic
# What is GAC ?
Back:


![[Pasted image 20221219060602.png]]
<!--ID: 1671497277980-->
ENDanki

STARTanki
Basic
# What are the important components of .NET framework(4 components )? What are their roles?
Back:

1. CLR - common language runtime
2. CTS - common type system
3. CLS - common lanaguage specification
4. FCL or BCL - Framework class Library
![[Pasted image 20221219060726.png]]
<!--ID: 1671497277989-->
ENDanki

STARTanki
Basic
# What is Enum keyword used for?
Back:


![[Pasted image 20221219060810.png]]
<!--ID: 1671497277999-->
ENDanki

STARTanki
Basic
# What is Garbage Collection(GC) ?
Back:

Garbage Collector is a back ground process which cleans ==unused
Managed== resources.

![[Pasted image 20221219060846.png]]
<!--ID: 1671497278008-->
ENDanki

STARTanki
Basic
# What is an Assembly? What are the 3 different types of assembly in .NET ?(PSS)
Back:

its something we get when we build the code. DLLs or EXE

![[Pasted image 20221219060952.png]]
<!--ID: 1671497278018-->
ENDanki

STARTanki
Basic
# Can we force Garbage Collector to run ?
Back:


![[Pasted image 20221219061022.png]]
<!--ID: 1671497278027-->
ENDanki

STARTanki
Basic
# What is the difference between Process and Thread?
Back:


![[Pasted image 20221219061050.png]]
<!--ID: 1671497278036-->
ENDanki

STARTanki
Basic
# What is the difference between “Finalize” and “Finally” methods?
Back:


![[Pasted image 20221219061119.png]]
<!--ID: 1671497278046-->
ENDanki

STARTanki
Basic
# What are Generations in garbage collection ? How many generations will be there?
Back:


![[Pasted image 20221219061231.png]]
<!--ID: 1671497278059-->
ENDanki

STARTanki
Basic
# What is the difference between “Dispose” and “Finalize”?
Back:


![[Pasted image 20221219061330.png]]
<!--ID: 1671497278069-->
ENDanki

