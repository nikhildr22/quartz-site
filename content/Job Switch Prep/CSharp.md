---
alias: []
Status: 
Medium: 
Tags: [dotnet,]
url: 
---
___
# CSharp



.net has no full form
it supports 30+ languages.

we cant use same lang for develop all kind of apps,
but
we can use the same env to develop desktop apps, web apps, mobile apps.

c# is the most popular language for .net framework.

almost 70% apps are either in java or c#.

why c#?
- OOPS
- Platform independent
- language independent

# visual studio ide
IDE specially for .net apps

every app is a project on visual studio
![[Pasted image 20221104111559.png]]
project name and solution name can be different.
single solution can have multiple projects inside it.

Namespace is a logical container to group classes.

By default, the project name is namespace .
```cs
using System;
using System.Collection Generic;
using System.Linq;
using System.Text;
using System. Threading. Tasks;
```

To use any class, we need to import the namespaces using **using** keyword

Solution explorer: where we can browse files inside the solution.

if we have multiple classes and multiple main methods, we can select the startup object to select the `Main` method to be run when app starts

![[Pasted image 20221104112735.png]]

# constructor
special method responsible to initialize the variable of the class.

name of constructor is same as class.
it does not return any value.

whenever we want to create an instance, its the responsibility of the programmer to define a constructor.

if not declared, the compiler will define a implicit constructor.

Implicit  constructors are also called as parameterless constructors.

constructors are public.

if we define a constructor, its called explicit constructor . tHIS CAN be parameterless or can have parameters.


# Types of constructors in csharp

> -  default or parameterless
> -  parameterized
> -  copy constructor
> -  static constructor


1. default  or parameterless 
	1. -If a constructor method doesn't take any parameters then we call that as default or parameter less. These constructors can be defined by a programmer explicitly or else will be default implicitly provided there is no explicit constructor under the class
2. parameterized
	1. connstructor with parameters, this can only be defined by programmer 
3. copy constructor
	1. Constructor has same class as parameter to it.
	2. ![[Pasted image 20221105060142.png]]
4. static constructor
	1. If a constructor is explicitly declared by using static modifier we call that as Static Constructor. All the constructors we have defined till now are non-static or instance constructors.
	2. it is defined explicitly
		1. 1. If a class contains any static variables then only implicit static constructors will be present or else we need to define them explicitly whereas non-static constructors will be implicitly defined in every class (except static class) provided we did not define them explicitly.
	3. they cant be parameterized , thus we cant overload them.
	4. Also they'll always be called implicitly even though we define them explicitly 
	5. This is the first block of clode that is executed inside  a class.

why we need explicit  constructor when we already have implicit constructor by default?


# static vs non static constructors
Static Constructors Vs Non-Static Constructors:
-If a constructor is explicitly declared by using a static
modifier we call that constructor as static constructor whereas
rest of other are non-static constructors only.
-Constructors are responsible for initializing fields/ variables of
a class, static fields are initialized by static constructors and
non-static fields are initialized by non-static constructors.



![[Pasted image 20221105061608.png]]

static constructors are implicitly called, but non static constructor should be called explicitly .

Static constructor run only once and even before we create an instance of that class.
but non static constructors run every time we create an instance of a class.

# variable of class, instance of class, reference of a class


every class is a user defined type.

instance is a copy of a class which can be used in our program.
instance of a class can be created using new keyword.

![[Pasted image 20221106035046.png]]

until we create a instance, the variable will be null.
Reference of a class:
![[Pasted image 20221106035312.png]]
f1 and f2 are using the same memory.
Reference of a class: a copy of the class that is
initialized by using an existing instance, and
references of class will not have any memory
allocation they will be sharing the same memory
of the instance that assigned for initializing the
variable.


reference of a class in c# can be called as pointer to a class.

# Access Specifiers

#todo 
- [ ] come up with a way to remember these 5 types and the differences, its every important in OOPs

- its a special kind of modifiers used to define scope of type and its members
- c# has 5 access specifiers 
	- private
	- internal
	- protected 
	- protected internal
	- public

Private members are not inherited can only be used inside within the class.
we cannot declare class as private, protected, protected internal.

case1: Same class
case2: Child class in same project
case3: non child class of same project
case4: child class of different project 
case5: non child class of different project,

![[Pasted image 20221106041109.png]]

Internal: accessible inside same project.
Protected: Accessible from same and Child class
Protected internal is OR condition between Internal and Protected.

**Default access specifier is Internal**


# different types of variables
- static variables
	- they dont need an instance for memory allocation and execution
- non static variables
	- they need an instance to need memory to be allocated and execution.
- constant variables
	- use keyword 'const' 
	- should be initialized while declaring.
	- cannot change the value
	- only one copy of const will present for a class, just like static variables
	- they dont need instance of class
	- only difference between static and const is mutability
- readonly variable :
	- just like const, this is immutable. 
	- but we can initialize  the readonly values inside constructors.
	- no need to initialize  while declaring .
	- every instance can have a different copy of readonly variable .
	- these are more similar to non static variables, but immutable .

**const is class constant, readonly  is instance constant.**

