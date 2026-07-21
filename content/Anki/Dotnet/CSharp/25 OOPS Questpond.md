
---
Created: 25th December 2022 05:37 AM
alias: []
Status: 
Medium: youtube 
Tags: [inbox, dotnet, ankied ]
url: https://youtu.be/u99wAoBjDvQ
links: 
---
___



STARTanki
Basic
# Why Object Oriented Programming?
Back:

it helps us think in terms of ==Real World Objects==

- Makes your code better
- Makes it readable
- Abstraction 
- Encapsulation
- Inheritance
- Polymorphism

>always try to give practical examples.(not silly examples like cat and dog, try to come up examples of your domain, **card, billing, user**)


![[Pasted image 20221225054127.png]]
<!--ID: 1672028464233-->
ENDanki

STARTanki
Basic
# 4 Pillars of OOP? (A PIE)
Back:

1. **Abstraction**: Show only what is necessary.
2. **Polymorphism**: :- Object acts differently under different conditions.
3. **Inheritance**: Parent Child relationship
4. **Encapsulation**: Hide complexity.


![[Pasted image 20221225054426.png]]
<!--ID: 1672028464240-->
ENDanki

STARTanki
Basic
# What is a class and object ?
Back:

Class is a type, blue print and object is a instance of the class.
<!--ID: 1672028464247-->
ENDanki

STARTanki
Basic
# Abstraction vs Encapsulation
Back:

- **Abstraction** :- Show only whats necessary.
- **Encapsulation** :- Hide complexity.


![[Pasted image 20221225054733.png]]
<!--ID: 1672028464253-->
ENDanki

STARTanki
Basic
# Explain Inheritance ? or what is  a `is a` keyword?
Back:

Inheritance defines a parent child relationship.
<!--ID: 1672028464259-->
ENDanki

STARTanki
Basic
# Explain virtual keyword ?
Back:

**Virtual** keyword helps us to define some logic in the parent class which can be overridden in the child class.
<!--ID: 1672028464265-->
ENDanki

STARTanki
Basic
# What is overriding ?
Back:

**Virtual** keyword helps us to define some logic in the parent class which can be **overridden** in the child class.
<!--ID: 1672028464271-->
ENDanki

STARTanki
Basic
# Explain overloading ?
Back:

Method overloading means same method names with different signature in the same class.
<!--ID: 1672028464277-->
ENDanki

STARTanki
Basic
# Overloading vs Overriding ?
Back:




Overloading :- Method with same names with different **signatures**.
Overriding :- Using virtual keyword and overriding in child class.
<!--ID: 1672028464283-->
ENDanki

STARTanki
Basic
# What is polymorphism ?
Back:

**Poly** means **Many** , **Morph** means **change as per
situation.**
==Its an ability of object to act differently under different condition.==
<!--ID: 1672028464289-->
ENDanki

STARTanki
Basic
# Can polymorphism work with out inheritance ?
Back:

**NO**
we need inheritence to achieve polymorphism.
![[Pasted image 20221225055222.png]]
<!--ID: 1672028464295-->
ENDanki

STARTanki
Basic
# Static vs Dynamic polymorphism ? compile time vs run time?
Back:

- Static polymorphism is implemented by Method overloading.
- Dynamic polymorphism is implemented by Method overriding.
<!--ID: 1672028464301-->
ENDanki

STARTanki
Basic
# Explain operator overloading ? how can we achieve  this?
Back:

Operator overloading helps to redefine additional functionalities for **plus**, **minus**, **multi** and **addition** operators.
This can be achived by defining a static class with operator keyword.
```cs
public static SomeClass operator +(SomeClass agr1, SomeClass arg2)
{
	//we'll return new object
	return new SomeClass ("//addition logic here")
}
```


![[Pasted image 20221225055351.png]]
<!--ID: 1672028464306-->
ENDanki

STARTanki
Basic
# Why do we need Abstract classes ?
Back:

Abstract class is a  ==half defined parent class.==
Impress the interviewer by saying ==**Partially defined**== :-)
characteristics if Abstract Class:
- pure half defined parent class.
- cannot create an instance of it.

Normal classes can not create PURE HALF DEFINED parent class
<!--ID: 1672028464313-->
ENDanki

STARTanki
Basic
# Are Abstract methods virtual ?
Back:


==YES==
<!--ID: 1672028464318-->
ENDanki

STARTanki
Basic
# Can we create a instance  of Abstract Classes? Can we inherit from Abstract CLass? Is it compulsory to implement Abstract methods?
Back:

Can we create a instance of Abstract Classes? ==No==
we can inherit from abstract class(single inheritence only)
Is it compulsory to implement Abstract methods? ==Yes==
<!--ID: 1672028464325-->
ENDanki

STARTanki
Basic
# Why simple base class cant replace Abstract class ?
Back:

simple base class can not be defined PURE HALF WAY.
<!--ID: 1672028464331-->
ENDanki

STARTanki
Basic
# Explain inheritence and why do we need it?
Back:

Interface is a CONTRACT

Having a tight contract means, you cannot change the interface without affecting the classes that are based on that interface.
Also, we cannot add extra properties/methods without telling the interface inside an inherited class.

![[Pasted image 20221225060137.png]]
<!--ID: 1672028464337-->
ENDanki

STARTanki
Basic
# Can we write logic in interface ? Can we define methods as private in interface ?
Back:

- it contain only signatures
- all properties and methods are public inside an interface.
![[Pasted image 20221226094011.png]]
<!--ID: 1672028464342-->
ENDanki

STARTanki
Basic
# If i want to change interface whats the best practice? OR What if i want to break contract of inheritence? 
Back:

==NEVER SAY YOU'LL MODIFY THE CURRENT INTERFACE==
we'll create new interface, and use **multiple inheritence** 
![[Pasted image 20221225062934.png]]
<!--ID: 1672028464347-->
ENDanki

STARTanki
Basic
# How to achive multiple inheritence in C#?
Back:

using interfaces
<!--ID: 1672028464353-->
ENDanki

STARTanki
Basic
# Explain Interface Seggregation principle ?
Back:

It is one of **SOLID** principles.
The Complete definition:
Interface is a contract , by having contract we have better control on impact analysis , change management and breaking changes.

Multiple inheritance helps to add new methods with out affecting the old interfaces.
<!--ID: 1672028464358-->
ENDanki

STARTanki
Basic
# Can we create instance of interface ?
Back:

No
<!--ID: 1672028464363-->
ENDanki

STARTanki
Basic
# Can we do Multiple inheritance with Abstract classes?
Back:

NO
<!--ID: 1672028464368-->
ENDanki

STARTanki
Basic
# can we make abstract class and interface behave similar?
Back:

![[Pasted image 20221225063204.png]]
<!--ID: 1672028464374-->
ENDanki
