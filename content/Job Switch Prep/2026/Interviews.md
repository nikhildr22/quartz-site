# https://www.bell.ca/
1. explain all OOPs, why use, what advantages
2. diffrent polymorphism with code example
3. why and when to use a interface and abstract class
4. Deep discussion on Liskov substitution principle
5. detailed discussion on which method will be overriden when you [[inherit and override a virtual class]] 
6. Middleware example, what and how and where you've used
7. Coding - [[find the numbers array adding up to a target number]]

# Eurofins
1. Write simple html to fetch a json result and display in page


# TCS
1. max 20 mins interview
2. tell me about yourself
3. difference between SP and Function
4. How do you optimize a SP
5. authentication and authorization on api side, I need to memorize the whole thing
6. difference between select and selectmany, gotta practice linq queries
7. how do you fetch millions of entries from a table pagination
8. did not know design patters
9. architecture of current project you are working
10. how do you implement a custom middleware
11.  tricky question on what if there are multiple  catch blocks for exception handling, will finally block be hit if there's a return or a throw exception within a catch block, what happens when there a generic catch block at the end and the try throws a known exception [[Exception handling]]

# CGI
1. auth lifecycle, refresh token why and how it works
2. project architecture
3. why use await async, thread pool, order of excecution of thread pool
4. which code runs first in a Typescript file
5. messed up angualr question, rxJs, state management, observables, promises even though i have studied them few days ago
6. Coding question to print 1st non repeating character in a string - use dictionary, but messed up this too `Nnikhil => k`
7. need to learn middleware implementation thouroughly [[Middleware]]
8. lost power in the middle of the call, idk how to manage that, had to move to another room with better light

# Digital Aptech
1. explain different between authentication and authorization, entire flow
2. authentication flow implementation
3. authorization flow implementation
4. whats your approach to optmize this query - `var orders = await _context.Orders.Include(x => x.OrderItems) .ToListAsync();`
5. how do you check and fix if a Order endpoint is taking 10000 requests at a time and is too slow
6. Lets say you need a endpoint for Orders, whats your approach to implement it. (start with defining tables, configurations, data models,. services, endpoints, web pages)
7. Lets say there Order, Inventory, Payment. how do you make sure there's no data loss when payment fails, what'd be your approach.
8. Lets say there's a invoice item, user A and User B modifies the same invoice at same time. what'd be your approach to prevent data loss.
9. how do you design database for this expense management system - ExpenseItem, employee, ExpenseClaim, Approval history
10. difference between switchmap, mergemap and concat map and when would you use it
11. when you are api's are already fast how would you improve the page loading times in angular, whats your approach for optimization
12. different scenarios of dependency injection , when and how'd you use it in backend
13. Middleware - why we need a middleware, have you implemented custom middle ware, can we use a middleware outside of http reques pipeline
14. coding - input: ["listen","silent","eat","tea","hello"] Output:[[listen,silent],[eat, tea],[hello]]

# SISA technologies
1. eager loading vs lazy loading in c#
2. difference between static class and interface where you'd use it
3. difference between abstract class and interface where you'd use it
4. whats a middleware
5. order of all middlewares inside program.cs
6. difference between first and firstOrDefault
7. difference between singleton and repository design pattern and where you've used in your project
8. Solid principles - explain few and where you've used in your project
9. difference between readonly and const variable in c#
10. difference  between iEnumerable and Iqueryable and whats the uses
11. why use Linq queries

# IBM
1. explain oops concept with examples and why use each concept
2. what is a middleware
3. what is the use of appsettings.json
4. how'd you refactor if I give you a legacy code base project
5. different data bindings in angular
6. difference between a stored procedure and a function
7. what is a view in sql, and why we need it
8. which is better for performance, stored procedure or function
9. dependency injection, what is it why we need it, what are some ways of achieving dependency injection
10. coding "hello" => h1e1l2o1

# CGI L2
1. api tokens how they work
2. multi token authentication, how do you generate tokens
3. what are the contents of a header file
4. whats a signature in header file
5. employees table
		id name mgrId skillset
		
		Nikhil > my manager -> super manager
		Write queury to fetch count of employees for all super managers
6. can you write code for how do you validate a custom api token
7. can you write code to show how data is passed between child and parent components in angualr
8. where have you used encapsulation in angular code
9. what are DOM and how do you implement a DOM element in angular

# Zemoso Labs
1. how'd you integrate a payment gateway
2. how'd you implement API for orders
3. write a custom middlware which logs the endpoint path and controller method
4. what'd be your approach to implement a logger
5. how'd you handle concurrency issues when multiple users are trying to modify the same record
6. implement code first approach write code

# Siemens technologies
1. they were mainly looking for a windows application developer role
2. what is OOPs why do we need it
3. solid priciples explain L and D in SOLID
4. write code for virtual and overriding
5. difference between const and readonly
6. what approach will you follow if you dont want to block the user when the screen freezes
7. consider 2 classes BaseClass DerivedClass, where DeviredClass Overrides a virtual method defined in BaseClass
	1. what are the outputs when we create objects like this
		1. BaseClass object1 = new DerivedClass();  
			1. this'll call derived class method
		2. BaseClass object2 = new BaseClass();  
			1. this'll call baseclass method
		3. DerivedClass object3 = new DerivedClass();  
			1. this'll call derived class method
		4. DerivedClass object4 = new BaseClass();
			1. A base class object cannot be stored in a derived class reference.
			2. Think of it like this:
				1. Every `DerivedClass` **is a** `BaseClass`.
				2. But every `BaseClass` is **not** a `DerivedClass`.

will method overloading work here?
```cs
public string Show(string a, string b)  
{  
  
}  
  
public int Show(string a, string b)  
{  
  
}
```

This **does NOT compile.**

## program to reverse a string
```cs
public static void ReverseString(string line)  
{  
	char[] charArray = line.ToCharArray();  
	  
	for (int i = 0; i < charArray.Length / 2; i++)  
	{  
		char temp = charArray[i];  
		charArray[i] = charArray[charArray.Length - 1 - i];  
		charArray[charArray.Length - 1 - i] = temp;  
	}  
	  
	Console.WriteLine(new string(charArray));  
}
```


# Neosoft solutions
1. Introduce yourself
2. what are triggers, how do you preevnt deletion using triggers
3. what is an SP, can you write a SP
4. what are magic tables
5. whats a middleware
6. explain authentication and authorization and how it works
7. complete auth flow from angular to web api
8. why we need switchMap on search field
9. how switchmap is different than merge map
10. exception handling 
	1. can we have multiple catch blocks
	2. how does the order of catch block affect and which catch block is triggered first
	3. what if catch block throws another error, will it override the first error
	4. what if catch block has return statement
	5. will finally block run if catch block throws error or has return statement
11. how do you find the unique character in this string using Linq - "programming"
12. If a API endpoint is getting 10000 requests at a time, how do you handle it


# Siemens Healthneer
1. [[Stack and heap for memory management]]
2. this was mostly standard interview questions which are in my notes but I havent studied yet.
3. 


# Chevron
1. explain the technical architecture of any of your project
2. how to implment content negotiation in web api(it wont happen automatically)
3. how does http interceptor on angualr work and what are the use cases
4. what are impure pipes
5. what are signals in latest angular and what problem they are solving
	1. how they are different from subject and behaviorsubjects
6. Linq Query to take a list of strings and print the 2nd largest string
7. returning multiple values from a method - use a touple

# IRCA Analytics - L2
1. JWT token contents
2. can same jwt for 2 users
3. iqueryable vs ienumerable which is best
4. managed unmanaged code
	1. how do you manage garbage in unmanaged code
5. garbage collection generations
6. thread safety
7. await async
8. how do you diagnose performance in running api on server
	1. do you know about dotnet dump file or run dump files?
9. Idempotency in rest api
10. why dbContext is scoped, what if we make it singleton
11. can middleware be singleton
12. difference between middleware and action filter
13. `List numbers = [1,2,3,4]; for i in list if i%2==0 numbers.Remove(i)` what will be the output of this and will it throw error.
14. roles vs claims within JWT
15. what solid principle is used for API versioning
16. difference between struct and record in c#
17. are class mutable?
18. how to send a certificate along with JWT
19. how do you handle streams
20. How do you handle n+1 problem in ef core
21. types of authorization

# Kyndryl
1. in and as keywords
2. sealed class
3. magic tables
4. delete vs truncate
5. SOLID
6. how authorization works
7. how to add new role to authorization
8. whats a middleware
9. whats the use of using `using` keyword
10. indexing in database
	1. how indexing works in Primary key is Guid
11. Was roasted for SQL
12. how do you do API versioning
13. explain OOPS
14. approaches of Dependency injection (not lifecyles)
15. 

# Cognizant
1. Dependency injection

# fnf
1. [[coding heavy on development, best practices FNF interview]]
2. explain solid, with examples
3. how do you use repository pattern write code for it
4. how do you write code for this - Banking -> account details -> transfer money -> amount > 0; // frontend -> get account and then transfer, security
	1. had to write entire boiler plate code and explain in an hour
5. SQL statement to get - top 3 custombers who tranferred highest total amount