---
Created: 5th January 2023 10:17 AM
alias: [mvc]
Status: 
Medium: 
Tags: [inbox, dotnet]
url: https://youtu.be/Ho508axF87Q
links: 
---
___
# Filters in MVC


What are filters?
What is the need of filters?
What are the different types of filter?
Predefined VS custom filters
Different ways to use filters
And lots of things...

Filters are different in MVC 4 and MVC 5

![[Pasted image 20230105101831.png]]

![[Pasted image 20230105101855.png]]

logic before the action method.

Filters are attribute which are used to perform some logic before, and after a action method is called.
Example —
	Caching
	Error handling
	Logging
	Permission (Authentication)
	Etc...

in MVC 4 we had 4 filters.

In MVC 5 there are 5 types of filters:
- Authentication filter
- Authorization filter
- Action filter
-  Result filter
- Exception filter
Note - This is also order of execution of all filters.

## Predefined filter
Some of the filters already built in asp.net mvc framework and
are ready to use.
Example:
	Authorize
	HandleError
	Validatelnput
	OutputCache
	Etc .

# Custom Filters-

Can we create own (Custom) filters?
**Yes**
As per requirement we can create custom filters for all 5 types of filter.

# Different places to use filter-
There are three place where we can use filter in asp.net mvc —
- Action method
	- written over  action
- Controller
	- written over controller
- Global
	- in global level for all controllers