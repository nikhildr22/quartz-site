---
Created: 2nd January 2023 09:34 AM
alias: [dotnet core web api]
Status: 
Medium: youtube 
Tags: [inbox, dotnet]
url: https://youtu.be/87oOF9Ve-KA
links: 
---
___

API can be interatced with other apps and not just GUI.

create a new project:
![[Pasted image 20230102093650.png]]

![[Pasted image 20230102094019.png]]
configure HTTPS  - always redirected to HTTPS

enable docker will- enable docker container support

Use controllers (uncheck to use minimal APIs)  - when we are not using controllers

Enable OpenAPl support --> this is for swagger support,

When we run it by default,
we get swagger UI to test the API.
![[Pasted image 20230102094121.png]]

we can also maintain versions of the APIs.
![[Pasted image 20230102094301.png]]
its good practice to have different versions. Its easy to release and rollback.

API sits between the UI and Data.

Mobile apps should not directtly talk to the database directly.
Because Mobile apps have entire code on the client side. Thus, it will also have the credentials to contact the db.
We cant allow the client to have the source code and the credentials to access the db as well.
Thus, if we have an API. Mobile apps can work with the help of API calls.

client will be having the ability to decrypt the data.

Other Js Apps built on angular/react can talk to the APIs to get the data.

Program.cs
![[Pasted image 20230102095948.png]]
![[Pasted image 20230102100021.png]]
we create our webApplication on line 1.
the add all services like controllers and dependancy injection.
add swagger service

Then we'll build the applicationThis line is saying to use swagger only in dev environment.
![[Pasted image 20230102100650.png]]
In launchsettings.json we can see the application lanch settings configured:
![[Pasted image 20230102100301.png]]

But this is only for Locally lanching the application.

But in production build, this launchsettings.json will not be there.
So, The Program.cs wont be able to find the config. so it assumes its in production.

if we want the swagger documentation to be visible to the client, instead of using if condition, just remove it.
![[Pasted image 20230102100701.png]]

![[Pasted image 20230102100714.png]]
these lines help us setup the pipeline for the requests.


Every controller will inherit from `ControllerBase` class

if we have just one Get method, it will be the default get method for that controller.

How to add a controller.
![[Pasted image 20230102101222.png]]
Dont choose MVC controllers, choose specifically the API controller.
![[Pasted image 20230102101259.png]]
give it a name.

![[Pasted image 20230102101508.png]]
there'll be a route for the controller.
it is annotated as APICOntroller.

![[Pasted image 20230102101654.png]]
we can overload get by making it expect a parameter.

We cant completely let it follow all REST guidelines, but we'll try to follow it.


What are minimal API's?
instead of writing endpoints in an controller. we'll write the code in Program.cs file itself.
But it'll not have any impact on the end user.
we can use inlfine fucntions/arrow functions
![[Pasted image 20230102102251.png]]

