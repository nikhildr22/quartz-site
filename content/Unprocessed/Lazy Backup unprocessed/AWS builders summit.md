#  Cloud security fundamentals: What every builder needs to know
![[Pasted image 20220714060634.png]]
![[Pasted image 20220714061145.png]]
![[Pasted image 20220714061346.png]]
with traditinal data center, you move faster OR you be more secure.
but with AWS, you can move more faster AND be more secure.

![[Pasted image 20220714061416.png]]

![[Pasted image 20220714061554.png]]
different compliances will be followed depending on the region:
![[Pasted image 20220714061835.png]]

![[Pasted image 20220714061936.png]]
AWS region is a cluster of data centers, in a certain geographic zone.

AWS will never move the data from one region to another without customer's conscent.

![[Pasted image 20220714062118.png]]

![[Pasted image 20220714062232.png]]

Data Protection:
![[Pasted image 20220714062446.png]]
![[Pasted image 20220714062506.png]]
mTLS - mutual TLS -> 2 stage verification that uses certification manager to verify the user. 

then API gateway will talk to the load balancer with TLS.
Load balancer will talk to containers with TLS.

COntainers can access data storages/db with TLS.

here also we can use mTLS.

Now coming to the data at Rest:
Object storage bucket will use Key Management service, which provides data key.
![[Pasted image 20220714063215.png]]

Identity & Access management:
![[Pasted image 20220714063337.png]]
![[Pasted image 20220714063410.png]]

RBAC etc

![[Pasted image 20220714063746.png]]
![[Pasted image 20220714064040.png]]
IAM Users -> long term
IAM Roles -> short lived

![[Pasted image 20220714064237.png]]

## demo
we use command line for this demo

---
![[Pasted image 20220714065244.png]]
![[Pasted image 20220714065309.png]]
![[Pasted image 20220714065649.png]]
![[Pasted image 20220714070025.png]]

---
---
# Session 2
# Choosing optimal compute
![[Pasted image 20220714070628.png]]
![[Pasted image 20220714070712.png]]
customers like to manage less.
![[Pasted image 20220714070806.png]]
![[Pasted image 20220714070950.png]]
Lambda service is for individual events.
containers are more like traditional computing.
But containers help to convert monolithic applications into more

![[Pasted image 20220714071136.png]]
![[Pasted image 20220714071241.png]]
![[Pasted image 20220714071355.png]]
Lambda is serverless
![[Pasted image 20220714071445.png]]
common use cases for Lambda.

![[Pasted image 20220714071556.png]]
![[Pasted image 20220714071712.png]]
![[Pasted image 20220714071740.png]]
here Event bridge is used for managing event driven architecture
![[Pasted image 20220714072018.png]]
![[Pasted image 20220714072033.png]]
![[Pasted image 20220714072048.png]]
![[Pasted image 20220714072103.png]]
![[Pasted image 20220714072121.png]]
![[Pasted image 20220714072142.png]]
![[Pasted image 20220714072218.png]]
![[Pasted image 20220714072356.png]]
![[Pasted image 20220714072650.png]]
![[Pasted image 20220714072730.png]]
![[Pasted image 20220714072935.png]]
![[Pasted image 20220714072948.png]]
![[Pasted image 20220714073107.png]]


---
---

# Session 3 Deploying your first web app 
![[Pasted image 20220714073728.png]]
![[Pasted image 20220714073737.png]]
![[Pasted image 20220714073857.png]]
![[Pasted image 20220714074000.png]]
![[Pasted image 20220714074107.png]]

this will be CICD .

![[Pasted image 20220714074635.png]]
![[Pasted image 20220714074707.png]]
![[Pasted image 20220714074834.png]]
![[Pasted image 20220714074955.png]]

---
![[Pasted image 20220714075424.png]]
![[Pasted image 20220714075458.png]]
![[Pasted image 20220714075513.png]]
![[Pasted image 20220714075521.png]]
![[Pasted image 20220714075533.png]]
![[Pasted image 20220714075629.png]]
![[Pasted image 20220714075855.png]]
![[Pasted image 20220714080007.png]]
![[Pasted image 20220714080203.png]]
![[Pasted image 20220714080250.png]]
![[Pasted image 20220714080256.png]]
![[Pasted image 20220714080329.png]]
