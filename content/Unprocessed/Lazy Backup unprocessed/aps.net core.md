---
alias: []
Status: 
Medium: 
Tags: 
url: https://youtu.be/1ck9LIBxO14
---
___
# aps.net core

![[Pasted image 20221216045141.png]]
give it a  name
![[Pasted image 20221216045215.png]]
![[Pasted image 20221216045249.png]]
this auth for smaller apps.
we need https checked when we have auth enabled.

![[Pasted image 20221216045356.png]]
MVC is a user interface layer.


`wwwroot` is where static files live.
![[Pasted image 20221216045803.png]]


In `Areas` identity system lives.

`Controllers` `Models` `Views`

`startup.cs` and `program.cs` --> where the app actually starts. these are console apps that starts web app and does configuration stuff.


`appsettings.json` its a replacement for `web.config` 

`program.cs`

# configure services

![[Pasted image 20221216045932.png]]
goto startup and look for startup configuration.


![[Pasted image 20221216045957.png]]
it uses dependency injection by default.
definining default connection for my dbContext.
![[Pasted image 20221216050033.png]]
![[Pasted image 20221216050051.png]]
we can change the connection string.

this is for identity information:
![[Pasted image 20221216050201.png]]

![[Pasted image 20221216050327.png]]
add controller and views.
but it also supports razor pages.



# configure method
![[Pasted image 20221216050439.png]]

![[Pasted image 20221216050513.png]]
define what to do in development mode.
![[Pasted image 20221216050549.png]]
this debug window is the place where we have configs setup for debug mode.
you can see the env variables are set to debug.

![[Pasted image 20221216050729.png]]

under `Properties` and `launchSetings.json` , we can we can see the run profiles set up.

![[Pasted image 20221216050925.png]]

![[Pasted image 20221216050934.png]]
-  redirect to https
- use static files in wwwroot
- add routing
- add auth
- add authorization
- define endpoints would look
- ![[Pasted image 20221216051146.png]]
	- map the route
	- ![[Pasted image 20221216051207.png]]
		- map the actual razor pages.


# why we are using mvc?
controllers and views can be tested differently.
you can test your logic without testing UI.


# Controller
it has a constructor.
![[Pasted image 20221216051400.png]]
it has a built in logging system.

always have a `Index` action
![[Pasted image 20221216051428.png]]

![[Pasted image 20221216051445.png]]
respective views are present here.

![[Pasted image 20221216051533.png]]
for error page, by default we can disable caching.

>Note that, bootstarp versions from MVC to mvc core are different, which might break UI, if you simply copy pages.

# models
they are always for displaying data.
dont use it as data transformation usage.
But there is no one right answer.

# data

![[Pasted image 20221216052201.png]]



