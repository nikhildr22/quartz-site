---
alias: []
Status: 
Medium: youtube
Tags: 
url: https://youtu.be/17Bl31rlnRM
---
___
# Docker
## What we had?
apps run on the servers.
only 1 app on one server in older days.
if the load increases, they had to add a new server and deploy app there.

VMware solved this issue with virtual machines.
This will help multiple systems on one server.

But VMware required a specific OS to run.
Thus there was a dependancy if we had to scale or migrate.

Also, setting up dependancies on a system is very tedious job.

## solution?
### Containers:
they help us run isolated application environment on the same OS.

Its just like a shipping container.
No matter what the contents are , we'll ship the container.
![[Pasted image 20220809205909.png]]

### is it platform dependent? Yes? But we can use WSL to overcome this problem in windows.

windows based docker cant run on linux based docker.

Thus we need WSL -> windowns subsystem for Linux.

so we'll use Windows+WSL 

in linux we can run as it is.

In max we need VM to run docker.


### Installation
download docker desktop for windows/mac

for linux, checkout installation manual on official site.


### parts
**Docker runtime**:
it helps us start and stop the containers.
2 types of runtime:
1. runC
2. container d

runC  is low level runtime, it works with OS and it helps in starting and stopping the containers.

ContainerD works in high level runtime.
It manages runC runtime, and also helps in networking of containers etc.

**Docker engine, daemon**

![[Pasted image 20220810101247.png]]
it works in client server architecture.

where docker daemon being the server.
and docker CLI being the client.

Whatever commands given to the CLI are passed to Server(daemon) to get the work done.


**Orchestration**:
This is used to manage group of docker containers.
docker swarm.
we'll use kubernetes to do this job.


### Container Image/ docker image

Its a file that contain all the instructions to run the application.

when we run the docker file, we'll get an Image.
When we run the Image, we'll get the container.

to share to others, we'll share the docker Image, not docker file.

its similar to class and object.
where docker image can be considered as a class and actual container can be similar to the object of that class.
==Its Just an Anology==



### OCI - Open container initiative
basic rules for docker file.


### Docker in DevOps

![[Pasted image 20220810102230.png]]


### Hello world
`docker run hello-world`

`run` -> to run an image to create a container.
`hello-world`  is image name.

 ![[Pasted image 20220810102554.png]]
 here, since we did not have this image locally, it'll search in online library/dockerhub and download the image.

Then it runs the downloaded image.

`docker run -it ununtu`

this'll run the `ubuntu` docker image in `-it`  interactive mode.

`docker images` -> it'll display all images present on my local machine.
![[Pasted image 20220810102921.png]]
if its already present in local machine, then it'll  run very fast.

https://hub.docker.com/
docker hub has all publicly shared images.

![[Pasted image 20220810104258.png]]
This is how the docker commands work.
if the image is not present locallly, it'll be pulled from the internet.

its awesome, you dont have to install anything, just get the container and run it, all config steps will be taken care by docker.

`docker pull ubuntu` -> it'll download the latest version of the image.

`docker container ls` -> list all the containers running

`docker ps` ->gives of list of docker processes

`docker stop <id of process>` -> this'll stop that docker process

`docker prune`-> delete the container.

`-d` to run containers in detached mode.
detached -> running in the background
![[Pasted image 20220810105400.png]]


- [ ] get a cheatsheet of docker commands (if required)

we can do port forwardng while running the container.
![[Pasted image 20220810224125.png]]
Here port 80 is forwarded to 8080

### Layers in Docker images
usually DOcker images are split into layers.

each layer has unique hash value.

Thus, whenever we are downloading new image, and it has common layers with existing images, that layer will be reused, now downloaded again.

- [ ] #todo/paused https://youtu.be/17Bl31rlnRM?t=5508

