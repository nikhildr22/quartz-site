![[Pasted image 20221004052928.png]]
make sure you mvc installed

![[Pasted image 20221004052953.png]]


# how to find the version of the project
![[Pasted image 20221004053143.png]]
in references, see the version of system.web.mvc

during runtime also we can fetch the version.


# creating mvc app

file new project => web mvc 4
use razor view engine

it'll have mVC folders.

on controller folder, add a controler by right clicking on folder and add controller.

![[Pasted image 20221004055317.png]]

when the controller/action is not found: we'll get this error
![[Pasted image 20221004055714.png]]

# controllers in MVC
![[Pasted image 20221004055858.png]]

by default iti'll goto index method.

to change the default behavior. goto global.asax
![[Pasted image 20221004060035.png]]

Application_start() method will be invoked.

in routeconfig.cs we have our default controller and action are defined.
![[Pasted image 20221004060208.png]]

![[Pasted image 20221004060309.png]]
--> the last parameter says the id we pass is optional. thus even if we dont pass any id, the webpage still works.

How to get Trace the requests done to the app?
![[Pasted image 20221004060909.png]]
this line will ignore controller/action/id format for this specific path.
i.e., path to see trace.

![[Pasted image 20221004061024.png]]
--> this is the trace path.
to enable this, we need to make changes in web.config and routeConfig.cs file.
![[Pasted image 20221004061120.png]]
--> inside web.config file, make this change.

# Views in MVC
![[Pasted image 20221004061251.png]]

views help us format the data instead of just returning raw data.

This was an insight why we need views, that was a great demo.

Rightclick on controller and add view, dont select any extra strictly typed options.

and in controller,
we can use ViewBag to pass data to the views.

![[Pasted image 20221004061949.png]]
using ViewBag, we can create dynamic objects on the run.
in the above code, we created a dynamic object `Countries` and assigned it with a list of strings.

This ViewBag  will be automatically passed to the view rendered in the action method.
Note that the return type of action `ActionResult` is the base class , so we can use it for most of the return type while web development.

![[Pasted image 20221004062225.png]]
`@` symbol is used to render C# code / razor syntax
![[Pasted image 20221004062318.png]]
--> views will be stored in this heirachy, for every controller there'll be different folder.
Thus, different controllers can have same named views.

>for best practices, we should always use strongly typed viewmodels to pass the data.

# ViewData and ViewBag

![[Pasted image 20221004062549.png]]
ViewBag lets us have dynamic properties.

compile timer error checking is not done for these 2, thus more error prone if we missspell the names / properties.


# Models in MVC
![[Pasted image 20221004062920.png]]
Models are added in Models folder, its just a class.

![[Pasted image 20221004063421.png]]
if we dont pass the object to the view, we'll get this error.

![[Pasted image 20221004063509.png]]
![[Pasted image 20221004063303.png]]


# data access using ENtity Framework
![[Pasted image 20221004063611.png]]
![[Pasted image 20221104104834.png]]

- [ ] Need to relearn entity framework [[Entity Framework Core]]

![[Pasted image 20221104103428.png]]

Add a class in models folder
![[Pasted image 20221104103558.png]]

- [ ] Learn sql server syntax by heart 


