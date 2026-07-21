


---
alias: [mvc, model view controller]
Status: 
Medium: youtube
Tags: [dotnet, ankied]
url: https://youtu.be/pXmMdmJUC0g
---
___
ENDanki

STARTanki
Basic
# Planning for interview prep:
Back:

![[Pasted image 20221219090425.png]]
<!--ID: 1672032780840-->
ENDanki

STARTanki
Basic
# what is asp.net mvc core
Back:

It's a open source . cross platform web development framework to develop web application created by Microsoft.
<!--ID: 1672032780865-->
ENDanki

STARTanki
Basic
# Differentiate between ASP.NET Webforms vs MVC vs MVC core ?
Back:

 pick 3 important points and answer.
1. cross platform
2. performance
3. simplification
4. cloud ready

![[Pasted image 20221219090521.png]]
<!--ID: 1672032780881-->
ENDanki

STARTanki
Basic
# explain mvc architecture
Back:

![[Pasted image 20221219090743.png]]
![[Pasted image 20221219090753.png]]
View is for display
Model contains business Logic

Controller binds Model and View.
<!--ID: 1672032780895-->
ENDanki

STARTanki
Basic
# what is wwwroot folder
Back:

wwwroot we store static contents
like HTML, CSS, JS files.
![[Pasted image 20221226104645.png]]
<!--ID: 1672032780907-->
ENDanki

STARTanki
Basic
# what is appsettings.json file?
Back:

Appsettings.json file helps to store config information.
its  json file.
![[Pasted image 20221226104706.png]]
<!--ID: 1672032780921-->
ENDanki

STARTanki
Basic
# How to read configurations from appsettings.json ?
Back:

![[Pasted image 20221219090939.png]]
we need to use IConfiguration Interface
To read config data from Appsettings.json , we use the IConfiguraton
object which is injected by MVC Core Depedency Injection framework.


![[Pasted image 20221219091031.png]]
this namespace.
<!--ID: 1672032780933-->
ENDanki

STARTanki
Basic
# What is dependency injection ?
Back:

DI is a practice of providing Dependent objects from outside rather that the class creating using the NEW keyword.
<!--ID: 1672032780949-->
ENDanki

STARTanki
Basic
# Why do we need dependency injection ?
Back:

What does interviewer wants to hear ?
1. By delegating object creation outside the caller we have better decoupled system.
2. Change at one place and the changes are reflected across the application seamlessly.
<!--ID: 1672032780964-->
ENDanki

STARTanki
Basic
# How do we implement dependency injection ?
Back:

What does the interviewer wants to hear ?
To implement DI we need to use provide DI objects in **ConfigureServices** Method using **Scoped**,  **Transient**. **Singleton**
==startup.cs==
![[Pasted image 20221226104950.png]]
<!--ID: 1672032780979-->
ENDanki

STARTanki
Basic
# what is the use of middleware in mvc?
Back:

MiddleWare helps to execute pre-processing logic before controller is executed. 
![[Pasted image 20221226105037.png]]
<!--ID: 1672032780992-->
ENDanki

STARTanki
Basic
# how do we implement middleware?
Back:

Answering to the interviewer in short sentence.
In Configure method we need to add the middleware in the request pipeline using
`app.UseMiddleWare<>` code.

normally we need middleware for authentication or authorization
## step 1 :
- Add the middle ware
![[Pasted image 20221219091532.png]]
## step 2
- Write the logic in the invoke method
- write preprocessing logic.
![[Pasted image 20221219091650.png]]

## step 3: add it in configure method in ==startup.cs==
![[Pasted image 20221219091753.png]]




------
<!--ID: 1672032781005-->
ENDanki

STARTanki
Basic
# What does startup.cs file do ?
Back:

Startup.cs file helps to configure Dependency Injection and MiddleWare.
In ConfigureServices we configure DI
In Configure we add Middlewares.
![[Pasted image 20221219091907.png]]
![[Pasted image 20221219091924.png]]
<!--ID: 1672032781019-->
ENDanki

STARTanki
Basic
# ConfigureServices vs Configure method?
Back:

Startup.cs file helps to configure Dependency Injection and MiddleWare.
In ConfigureServices we configure DI
In Configure we add Middlewares.

![[Pasted image 20221219091907.png]]
![[Pasted image 20221219091924.png]]




----
<!--ID: 1672032781033-->
ENDanki

STARTanki
Basic
# Explain the different ways of doing DI? 
Back:


## addscoped
Instantiates once per request made to server
![[Pasted image 20221219092122.png]]

## addtransient
Instantiates every singletime service/object is injected.
![[Pasted image 20221219092157.png]]

## addsingleton
Instantiates once in an application life time
![[Pasted image 20221219092227.png]]

![[Pasted image 20221219092609.png]]
<!--ID: 1672032781047-->
ENDanki

STARTanki
Basic
# Explain Scoped vs Transient vs Singleton ?
Back:



## addscoped
Instantiates once per request made to server
![[Pasted image 20221219092122.png]]

## addtransient
Instantiates every singletime service is injected.
![[Pasted image 20221219092157.png]]

## addsingleton
Instantiates once in an application life time
![[Pasted image 20221219092227.png]]

![[Pasted image 20221219092609.png]]
<!--ID: 1672032781060-->
ENDanki

STARTanki
Basic
# What is Razor ?
Back:

Razor is a view Engine in which
we can write HTML and C# /
VB.NET code together.

it helps us to write server side code and html 
![[Pasted image 20221219092723.png]]
<!--ID: 1672032781073-->
ENDanki

STARTanki
Basic
# How to pass Model to a View ?
Back:


![[Pasted image 20221219092833.png]]

--------
<!--ID: 1672032781085-->
ENDanki

STARTanki
Basic
# Explain Strongly typed views ?
Back:

Strongly typed views are Razor views
where we get Model intellisense.
![[Pasted image 20221226105410.png]]
![[Pasted image 20221219092853.png]]



--------
<!--ID: 1672032781099-->
ENDanki

STARTanki
Basic
# What are viewModels ?
Back:

data which view needs.

we cant pass 2 models to a view, so we need a view model, which represents the data for that particular view.

its a wrapper class.
![[Pasted image 20221219093042.png]]
here, customerviewmodel is a wrapper class.
<!--ID: 1672032781113-->
ENDanki

STARTanki
Basic
# What is kestrel ?
Back:


free Open source web server comes with asp .net core..
![[Pasted image 20221219093139.png]]
<!--ID: 1672032781126-->
ENDanki

STARTanki
Basic
# Why Kestrel when Microsoft already had IIS ?
Back:

because .net core should run on cross platform.
<!--ID: 1672032781140-->
ENDanki

STARTanki
Basic
# does kestrel replace IIS
Back:

No.
because other servers like IIS, Apache have been since very long and have a lot of security features etc.
so While deploying, we'll use **reverse proxy** to use IIS and kestrel together.


![[Pasted image 20221219093401.png]]



-----------
<!--ID: 1672032781153-->
ENDanki

STARTanki
Basic
# What are cookies ?
Back:


text files stored in client browser containig information about the website
![[Pasted image 20221219093507.png]]
<!--ID: 1672032781167-->
ENDanki

STARTanki
Basic
# What is session management ?
Back:

HTTP is a stateless protocol.
every new request is  a standalone requuest.
**Session management techniques helps to maintain states between HTTP requests.**
![[Pasted image 20221219093602.png]]
<!--ID: 1672032781180-->
ENDanki

STARTanki
Basic
# What are the different ways of doing Session management ?
Back:



1. using session variable
	1. ![[Pasted image 20221219093719.png]]
2. viewdata/ ViewBag
3. TempData
<!--ID: 1672032781192-->
ENDanki
