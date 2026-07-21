---
Created: 29th December 2022 05:20 AM
alias: []
Status: 
Medium: 
Tags: [inbox, ankied, dotnet]
url: 
links: 
---
___
# Custom questions


STARTanki
Basic
Difference beween Generics and Generic Collections?
Back: 
![[Pasted image 20221229052248.png]]

## Problem with Array and ArrayList

**Array**

-   Arrays are strongly typed (meaning that you can only put one type of object into it).
-   Limited to size (Fixed length).

**ArrayList**

-   ArrayList are strongly typed.
-   Data can increase on need basis.
-   It will do the boxing and unboxing while processing (decrease the performance).

**List (Generic Collection)**

-   List are strongly typed.
-   Data can increase on need basis.
-   Don't incur overhead of being converted to and from type object.

A generic collection is strongly typed (you can store one type of objects into it) so that we can eliminate runtime type mismatches, it improves the performance by avoiding boxing and unboxing.

## Generic

Generic is the key concept to develop Generic collection.
<!--ID: 1672271606370-->
ENDanki


STARTanki
Basic
How do you configure routes in .NET core

Back: 
![[Pasted image 20221229060214.png]]
<!--ID: 1672273944236-->
ENDanki

STARTanki
Basic
What are filters

Back: 
Filters are attribute which are used to perform some logic before, and after a action method is called.
Example —
	Caching
	Error handling
	Logging
	Permission (Authentication)
	Etc...
<!--ID: 1672894756900-->
ENDanki

STARTanki
Basic
Syntax of ViewBag vs ViewData
Back: 
note that even though the viewbag with the term "Bag" might resemble to `[]` square brackets. It uses dot operator.
```cs
ViewBag.OutDynamicDataObject

ViewData["OurDynamicDataObject"]
```
<!--ID: 1673048376316-->
ENDanki

STARTanki
Basic
# how to use content negotiation using httpClient in web api
Back: 
```cs

client.BaseAddress = new Uri("https://api.example.com/");
            
            // 🔑 Content Negotiation: Request JSON
            client.DefaultRequestHeaders.Accept.Clear();
            client.DefaultRequestHeaders.Accept.Add(
                new MediaTypeWithQualityHeaderValue("application/json"));

            HttpResponseMessage response = await client.GetAsync("products");

```
<!--ID: 1756915303175-->
ENDanki










