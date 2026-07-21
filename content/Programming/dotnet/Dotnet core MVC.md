this is the same guy from bootstrap!!

TOC:
![[Pasted image 20210607032312.png]]

# course intro
![[Pasted image 20210607032428.png]]
## what to expect
![[Pasted image 20210607032450.png]]
![[Pasted image 20210607032505.png]]
![[Pasted image 20210607032537.png]]
we'll be building the same Pie shop as in bootstrap tutorial.

## what is asp .net core
![[Pasted image 20210607032804.png]]
![[Pasted image 20210607032940.png]]
![[Pasted image 20210607033008.png]]
![[Pasted image 20210607033111.png]]
this course focuses on MVC framework.

# Setup and configuring our site
## project structure
![[Pasted image 20210607034117.png]] 
select empty insde that
![[Pasted image 20210607034158.png]]
![[Pasted image 20210607034210.png]]
this is project structure
![[Pasted image 20210607034328.png]]

## configuring project

![[Pasted image 20210607034416.png]]
it'll create a host and confgure startup class

![[Pasted image 20210607034534.png]]
ConfigureServices:
here we'll configure the services through --> ![[dependancy injection]]
![[Pasted image 20210607034743.png]]

Configure method
![[Pasted image 20210607035255.png]]
it'll configure request-respnce pipeline
![[Pasted image 20210607035325.png]]

![[Pasted image 20210607035339.png]]
the order of these components is very necessary.
![[Pasted image 20210607035430.png]].

The statup of App:
![[Pasted image 20210607035516.png]]
this line for using mvc : ![[Pasted image 20210607035818.png]]
only in dev environment show Exception page : ![[Pasted image 20210607035927.png]]

middleware that redirects to  https : ![[Pasted image 20210607040019.png]]
 use static files: ![[Pasted image 20210607040043.png]]
 
 configuring default route: ![[Pasted image 20210607040129.png]]
 
 # Creating a List Page using mvc
 ## hello MVC
 ![[Pasted image 20210607040416.png]]
 ![[Pasted image 20210607040456.png]]
 asp .net core mvc is built upon asp .net core.
 ![[Pasted image 20210607040550.png]]
 ## creating the model and repository
 ![[Pasted image 20210607040612.png]]
 make sure the folder names are exactly as per standards.
![[Pasted image 20210607040657.png]]
![[Pasted image 20210607040716.png]]
![[Pasted image 20210607040732.png]]
![[Pasted image 20210607040743.png]]
![[Pasted image 20210607040800.png]]
and here as we discussed earlier, instead of using tight coupling,
we'll use dependancy injection. (loosely coupled code)
![[Pasted image 20210607040931.png]]
![[Pasted image 20210607040956.png]]
>note that `services.AddMvc();` is for older .net core versions

Registration options:
![[Pasted image 20210607041134.png]]
AddTransient --> everytime a new clean instance is returned
AddSingleton --> everytime the same instance is returned
AddScoped --> creates instance once per http request, and uses the same instance for other calls within the same web request.

 ## creating the controller
 ![[Pasted image 20210607043456.png]]
 ![[Pasted image 20210607043506.png]]
 controller name is suffixed by controller.
 ![[Pasted image 20210607043532.png]]
 
 ![[Pasted image 20210607043555.png]]
 ## adding the view
![[Pasted image 20210607043907.png]]
![[Pasted image 20210607043916.png]]
![[Pasted image 20210607043937.png]]
![[Pasted image 20210607043947.png]]
![[Pasted image 20210607044000.png]]
viewBag can be used to add data to view dynamically from the controller.
![[Pasted image 20210608042153.png]]
`@` --> razor syntax
![[Pasted image 20210608042226.png]]
![[Pasted image 20210608042245.png]]
![[Pasted image 20210608042315.png]]
viewmodel:
![[Pasted image 20210608042333.png]]

`@model <datatype of view>`
![[Pasted image 20210608042551.png]]
when we want to pass multiple values along with the models,
use ViewBag

>for the best practice, instead of using viewbag, create viewmodels and pass them to the view

code with viewmodel:
![[Pasted image 20210608042822.png]]

`_Layout.cshtml`
![[Pasted image 20210608042902.png]]
![[Pasted image 20210608042911.png]]
`@RenderBody()`--> place where the body will be placed.
![[Pasted image 20210608042959.png]]
`_ViewStart.cshtml` --> automatically called whenever a view is rendered.

`View Imports`--> ![[Pasted image 20210608043126.png]]
for imports

>for creating custom views --> select **Razor View**
>for creating layouts --> select **Razor Layout**
>for viewstart --> select **Razor Viewstart**
>for ViewImport --> select **Razor View Imports**




 
 
 ## styling the view
 vs 2019 comes along with Library manager.
![[Pasted image 20210608043813.png]]

### Adding client side packages using library manager
Adding Bootstrap :
![[Pasted image 20210608044026.png]]
right click on the project and select Add Client side Library,
search for twitter bootstrap
keep it in `wwwroot/lib/bootstrap` folder
click on install.

Now, Add jQuery in the same way ![[Pasted image 20210608044229.png]]

`images` --> folder contains images
`css` --> folder for css files
importing those libraries:
![[Pasted image 20210608044321.png]]


# Adding EF core
## Hello Ef core
![[Pasted image 20210608044817.png]]
[how to perform db first](https://stackoverflow.com/a/59815898/10841074)

![[Pasted image 20210608045318.png]]
![[Pasted image 20210608045329.png]]
EF core uses some conventions.

![[Pasted image 20210608045425.png]]
![[Pasted image 20210608045434.png]]
![[Pasted image 20210608045502.png]]
![[Pasted image 20210608045512.png]]
![[Pasted image 20210608045524.png]]
## Adding EF core to the application
from nuget packages 
install tools and sqlserver
### Add DbContext
![[Pasted image 20210608045703.png]]
### Add connectionstrngs
![[Pasted image 20210608045733.png]]
### ConfigureServices
as we know, our connection string is in appsettings.json file,

appsettings.json  is a special file which is mapped using IConfiguartion interface.
![[Pasted image 20210608045928.png]]
![[Pasted image 20210608045954.png]]
### querying the data
![[Pasted image 20210608050015.png]]
this code will be converted to most optimal sql statement and the data is fetched from the database.

For Saving Changes: ![[Pasted image 20210608050126.png]]

### adding repository
create a IRepository interface
Implement that interface in a Repository class.

Add the dependancy injection inside the startup.cs file.

![[Pasted image 20210608050407.png]]
make sure u use the development env to get the relevant errors while developing.
## Initializing the database
![[Pasted image 20210608050447.png]]
![[Pasted image 20210608050519.png]]

`add-migration <migrationName>`
it'll create a migration

`update-database` --> create a database

## Modifying the model

![[Pasted image 20210608050835.png]]

# Adding Navigation to site
## routing in mvc
![[Pasted image 20210608051441.png]]
![[Pasted image 20210608051506.png]]
![[Pasted image 20210608051548.png]]
![[Pasted image 20210608051639.png]]
![[Pasted image 20210608051646.png]]
![[Pasted image 20210608051659.png]]
![[Pasted image 20210608051705.png]]

## configure routing
![[Pasted image 20210608051724.png]]
![[Pasted image 20210608051812.png]]
![[Pasted image 20210608051830.png]]
![[Pasted image 20210608051951.png]]
![[Pasted image 20210608052020.png]]
![[Pasted image 20210608052032.png]]

## navigation with tag helpers
![[Pasted image 20210608052144.png]]
![[Pasted image 20210608052214.png]]
![[Pasted image 20210608052226.png]]
![[Pasted image 20210608052253.png]]
![[Pasted image 20210608052303.png]]
![[Pasted image 20210608052339.png]]

![[Pasted image 20210608052804.png]]




