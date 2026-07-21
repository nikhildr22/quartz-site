
---
Created: 24th December 2022 05:14 AM
alias: [interview questions, web api]
Status: 
Medium: 
Tags: [inbox, dotnet, ankied ]
url: https://youtu.be/FySr1tusL8c
links: 
---


STARTanki
Basic
# What is Web API? What is the purpose of Web API?
Back:

Web API(Application Programming Interface) provides interaction BETWEEN software applications.
why we need it? logic at common place can help you loosely couple backend and front end.
![[Pasted image 20221226095514.png]]
<!--ID: 1672031433440-->
ENDanki

STARTanki
Basic
# What are Web API advantages over WCF and web serivces?
Back:

Every business like amazon, facebook, twitter needs both mobile app
and website and Web API is a better option for that.
1. It works the way HTTP works using standard HTTP verbs like GET, POST, PUT, for all the crud operation.
2. It is an OPEN source.
3. It is a LIGHTWEIGHT architecture and is good for devices, which have limited bandwidth(JSON & XML are lightweight) like smart cell phones.
4. Web API Controller pattern is much similar to MVC Controller. Thus, it becomes easy to maintain and understand.
5. Web API has very easy configuration settings as comparison to WCF
![[Pasted image 20221226095801.png]]
<!--ID: 1672031433457-->
ENDanki

STARTanki
Basic
# What is Rest and Restful?
Back:


**REST stands for Representational State Transfer.**
REST is a set of guidelines which helps in creating a system where applications can easily communicate with each other.

**RESTFUL**: If a system written by architectural concepts, it is called RESTful services.
<!--ID: 1672031433476-->
ENDanki

STARTanki
Basic
# What are REST Guidelines 
Back:

1. **Separation of Client and Server** - The implementation of the client and the implementation of the server can be done independently without each knowing about the other.
2. **Stateless** - The server will not store anything about the latest HTTP request the client made. It will treat every request as new. No session, no history.
3. **Uniform interface** — Identify of resources by URL www.abc.com/api/questions
4. **Cacheable** - The cacheable constraint requires that a response should implicitly or explicitly label itself as cacheable or non-cacheable.
5. **Layered system** - The layered system style allows an architecture to be composed of hierarchical layers. For example, MVC is a layered system.

![[Pasted image 20221226102334.png]]
   
<!--ID: 1672031433496-->
ENDanki

STARTanki
Basic
# Is it possible to use WCF as Restful services?
Back:

Yes, we can develop RESTful services with WCF.
<!--ID: 1672031433513-->
ENDanki

STARTanki
Basic
# What are HTTP verbs or HTTP methods?
Back:

![[Pasted image 20221226102450.png]]
<!--ID: 1672031433529-->
ENDanki

STARTanki
Basic
# How to consume Web API from a .NET MVC application?
Back:

Web API methods can be consumed with the help of ==HttpClient== class.

![[Pasted image 20221224052201.png]]
<!--ID: 1672031433545-->
ENDanki

STARTanki
Basic
# What is the difference between Web API and MVC Controller?
Back:

![[Pasted image 20221226102657.png]]
<!--ID: 1672031433561-->
ENDanki

STARTanki
Basic
# What is Authentication?
Back:

Authentication means verifying a user who is accessing the system.
<!--ID: 1672031433576-->
ENDanki

STARTanki
Basic
# What is Basic Authentication in Web API?
Back:

Authentication means verifying a user who is accessing the system or Web API.

1. In Basic Authentication, the user passes their credentials (user name and password) on a **POST** request.
2. At the WebAPl end, credentials are verified.
3. If the credentials are valid, then a session will initiate to accept the subsequent requests without validating the user again.
![[Pasted image 20221226102941.png]]
<!--ID: 1672031433591-->
ENDanki

STARTanki
Basic
# What is API Key Authentication in Web API?
Back:

API Key Authentication
In API Key Authentication, the API owner will share an API key with the users and this key will authenticate the users of that API.
![[Pasted image 20221226103030.png]]
<!--ID: 1672031433608-->
ENDanki

STARTanki
Basic
# What is Token based authentication? V. IMP.
Back:


Token-based authentication is a 4 step process:
1. Client application first sends a request to Authentication server with a valid credentials.
2. The Authentication server/ Web API sends an Access token to the client as a response. This token contains enough data to identify a particular user and it has an expiry time.
3. The client application then uses the token to access the restricted resources in the next requests until the token is valid.
4. If the Access token is expired, then the client application can request for a new access token by using Refresh token.
![[Pasted image 20221226103223.png]]


OAuth is a standard for creating token based authentication and
authorization.
<!--ID: 1672031433622-->
ENDanki

STARTanki
Basic
# What is OAuth?
Back:


OAuth is a standard for creating token based
authentication and authorization.
![[Pasted image 20221224052534.png]]
<!--ID: 1672031433638-->
ENDanki

STARTanki
Basic
# What is JWT Authentication? V. IMP.
Back:


JWT authentication is a token based authentication where JWT is a token format.
JWT token -  JSON Web Tokens

![[Pasted image 20221224052559.png]]
<!--ID: 1672031433654-->
ENDanki

STARTanki
Basic
# What are the parts of JWT token?
Back:

JWT token - JSON Web Tokens
4 parts:
1. Algorithm used to generate the token.
2. The type of the token, which is JWT here.
3. The payload contains the CLAIMS.
4. The signature is used to verify that the issuer of the JWT correct.

![[Pasted image 20221224052719.png]]
<!--ID: 1672031433672-->
ENDanki

STARTanki
Basic
# Where JWT token reside in the request?
Back:

In REQUEST HEADER.
KEY - Authorization
VALUE - Token

![[Pasted image 20221224052750.png]]
<!--ID: 1672031433684-->
ENDanki

STARTanki
Basic
# How to test Web API? What are the tools?
Back:

![[Pasted image 20221224052802.png]]
<!--ID: 1672031433696-->
ENDanki

STARTanki
Basic
# What are main Return Types supported in Web API?
Back:


A Web API controller action method can return following types:
1. **Void** — It will return empty content.
2. **HttpResponseMessage** - It will convert the response to an HTTP message.
3. **IHttpActionResult** - internally calls ExecuteAsync to create an HttpResponseMessage.
4. **Other types** - You can create your own custom return type.
<!--ID: 1672031433710-->
ENDanki

STARTanki
Basic
# What is the difference between HTTPResponseMessage and IHttpActionResult?
Back:

In web API version 1.0, We have a type called **HttpResponseMessage** for receiving Http response message from API call.
In Web API version 2.0, **IHttpActionResult** introduce which is basically the replacement of HttpResponseMessage. It creates clean code and also simplifies unit testing.
![[Pasted image 20221224052915.png]]
<!--ID: 1672031433726-->
ENDanki

STARTanki
Basic
# What is Content Negotiation in Web API? V. IMP.
Back:


Whenever we consume an API, we receive data in either JSON or XML or plain text or your own custom format.
client can negotiate with server with the type of data it is expecting.
![[Pasted image 20221224053003.png]]
<!--ID: 1672031433741-->
ENDanki

STARTanki
Basic
# What is MediaTypeFormatter class in Web API?
Back:

**MediaTypeFormatter** is an **abstract** class from which **JsonMediaTypeFormatter** and **XmlMediaTypeFormatter** classes inherits.
![[Pasted image 20221224053037.png]]
<!--ID: 1672031433755-->
ENDanki

STARTanki
Basic
# What are Response Codes in Web API?
Back:


![[Pasted image 20221224053149.png]]
<!--ID: 1672031433767-->
ENDanki


