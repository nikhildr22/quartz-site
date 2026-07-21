---
Created: 28th December 2022 09:28 AM
alias: [authentication]
Status: 
Medium: youtube 
Tags: [inbox, dotnet]
url: https://youtu.be/bWA-pZJrOFE
links: 
---
___
# JWT Token using MVC Core


it is used for token based authentication .
token is more like a ticket.
its just like how we go to a movie and get a ticket.
for the first time, client needs to send user name and password for the first time.
once authentication is done, client will use this token for all the future requests.

How do we generate this token?
please dont write custom algorithm.
use built in algorthms to generate token.


# How to generate using asp .net mvc core.

Things needed:
1. existing valid credentials
2. algorithm()
	1. authentication is done using credentials 
3. authorization (claims/Roles) is can also be done using this.
4. Secret key/Salt
5. Constraints
	1. expiry
	2. who created it etc

Algorithm+Key = our Token/Bearer.

Make sure you keep your key in a secret place.

![[Pasted image 20221228094009.png]]



