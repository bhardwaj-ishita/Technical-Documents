# docker:

### what is concept of a container?

a way to package an application with all necessary dependencies and configurations. (putting a whole project inside a package)

portable artifact(easily shared and moved around)

makes development more efficient

containers stored in container repositories : private/public repositories (docker hub)

##### application development:-

| before containers                                            | after containers                                             |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| had to download the configurations every time a new person needs to use the application | don't have to install any of the services directly on your OS. everything is packaged one isolated environment |
| installation process different on each OS environment        | container is an own isolated OS. one command to install the app and it will run on its own |

two different versions of the same application can be run without creating any conflict



##### application deployment:-

| before containers                                            | after containers                                             |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| development team builds artifacts->instructions to install and configure  artifacts on servers ->jar files -> database with instructions -> all this given to operations team and send them for deployment | operations and developer team works in the same team         |
| miscommunication between between development team and operations team | the whole process is  configured to one single environment there is no need to configure any of this directly to the server |

run docker command and pulls the container

### what is a container, technically?

layers of stacked images

at the base is a linux base image (alpine 3.10) 

base image needs to be small so the container remains small

above it is application image

![image-20210511134556578](C:\Users\ishit\AppData\Roaming\Typora\typora-user-images\image-20210511134556578.png)

all these hashes are just images stacked up on each other

the *docker run postgress:9.6* fetches the image but also runs it directly after pulling it

##### docker image vs container:-

| docker image(not running)                                    | docker container(running)                                    |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| it is the actual package with configurations and dependencies | container is the image i pulled to the local machine and started it |
| artifact that can be moved around                            | container environment is then created                        |
| all artifacts in the docker hub are images                   | container is a running environment for the image (part of the container runtime) |
| they have tags or versions                                   | container has a port binded to it hence we can talk to the application running inside of container |
| make a container of the image to make it running             | the file system is virtual in the container; has its own abstraction of an OS, including the file system and environment which is different from  file system and environment of the host machine |
|                                                              |                                                              |

![image-20210511140001768](C:\Users\ishit\AppData\Roaming\Typora\typora-user-images\image-20210511140001768.png)

![image-20210511143317691](C:\Users\ishit\AppData\Roaming\Typora\typora-user-images\image-20210511143317691.png)

pulled postgres 9.6, postgres 10.10 and postgres 11.11

some of the layers are the same so don't need to download them again

![image-20210511140322927](C:\Users\ishit\AppData\Roaming\Typora\typora-user-images\image-20210511140322927.png)

this is the container running

now 2 different versions of postgres are running on different tabs without any conflict

### docker v/s virtual machine

OS has 2 layers

layer 1: OS kernel (communicates with hardware components; applications run on kernel layer)
layer 2: application layer  

docker and vm both are virtualization tools

for eg: in linux the OS kernel is same for ubuntu, fedora etc etc but the application layer is different

| docker                                                       | virtual machines                                     |
| ------------------------------------------------------------ | ---------------------------------------------------- |
| docker virtualizes the applications layer and uses kernel of the host | whereas vm has it's own application and kernel layer |
| size of docker image is much smaller(megabytes) as they have to implement only one layer | couple of gigabytes large                            |
| docker containers start and run much fast                    | for vm need to boot the system and run then run it   |
| compatibility: can't do that on docker<br want to run linux based docker on windows not compatible/> hence download a docker toolbox | run vm image of any OS on any other OS host          |

installation of docker differ based on the OS but also its version

### docker basic commands

```dockerfile
docker stop *container ID* (stops an active container)
docker rm *container ID* (removes the specified containers dead)
docker kill *container ID*  (kills the container)
docker rm $(docker ps -a -q) (removes all existing containers dead)
```

(-a -q can also be written as -aq)
pull, run, start, stop, ps (basic commands)



##### 1. docker pull

![image-20210513172746381](C:\Users\ishit\AppData\Roaming\Typora\typora-user-images\image-20210513172746381.png)

```dockerfile
docker pull redis 
```

(when version not specified then image pulled is of the latest version) 

here the image is pulled from the docker hub which is a public repository to the local environment

##### 2. docker images

![image-20210513172924410](C:\Users\ishit\AppData\Roaming\Typora\typora-user-images\image-20210513172924410.png)

```dockerfile
docker images
```

 (gives a list of all the images pulled till date)



##### 3. docker run

![image-20210513173020767](C:\Users\ishit\AppData\Roaming\Typora\typora-user-images\image-20210513173020767.png)

```dockerfile
docker run redis
```

 (converts the image to a container to run the program)

now latest version of redis is running on the terminal

docker run = docker pull + docker start



##### 4. docker ps

![image-20210513173141878](C:\Users\ishit\AppData\Roaming\Typora\typora-user-images\image-20210513173141878.png)

```dockerfile
docker ps
```

 (tells the running containers on the system along with the port container id etc)

###### -a

![image-20210513175019350](C:\Users\ishit\AppData\Roaming\Typora\typora-user-images\image-20210513175019350.png)

```dockerfile
docker ps -a
```

 (lists **all** the containers no matter stopped or running or exited)

##### 5.  ctrl + c

![image-20210513173343473](C:\Users\ishit\AppData\Roaming\Typora\typora-user-images\image-20210513173343473.png)

ctrl + c (to end the running container)
gives some message



##### 6. docker start/stop

![image-20210513174344107](C:\Users\ishit\AppData\Roaming\Typora\typora-user-images\image-20210513174344107.png)

```dockerfile
docker stop *container id*  (want to stop a container)

docker start *container id* (want to start a stopped container)
```

makes it possible to restart a container



##### 7. docker run (continued)

![image-20210513175600401](C:\Users\ishit\AppData\Roaming\Typora\typora-user-images\image-20210513175600401.png)

```dockerfile
docker run
```

 (pulls and runs the image together simultaneously)

![image-20210513175517533](C:\Users\ishit\AppData\Roaming\Typora\typora-user-images\image-20210513175517533.png)

two different versions of redis containers are running now

######  -d

![image-20210513174117729](C:\Users\ishit\AppData\Roaming\Typora\typora-user-images\image-20210513174117729.png)

![image-20210513174139973](C:\Users\ishit\AppData\Roaming\Typora\typora-user-images\image-20210513174139973.png)

```dockerfile
docker run -d redis
```

 (to start an ended container in a de attached mode)

###### -p

binds port of the host to the container

```dockerfile
docker run -p6000:6379 -d redis
```



##### 8. container ports VS host port:-

the port tells from which port the container is listening to the incoming requests from

both redis versions containers are from the same ports

how does this does not create conflict

containers is just a  vm running on your machine and can run simultaneously many ports

our laptop has certain ports 

so now what happens is we can can bind only one port to the host machine
but we can bind the same container port to two different local host port to make it work. As long as they are binded to different ports, your different versions of the same image will run

local port 5000 ---> port 5000 container

local port 3000 ----> port 3000 container

local port 3001 ----> port 3000 container

**here two containers are getting info from the same port but are binded to  different ports from the host machine**

once the binding is done you can actually connect to the running container from the port of the local host

some-app://localhost:3001

![image-20210513195417258](C:\Users\ishit\AppData\Roaming\Typora\typora-user-images\image-20210513195417258.png)

right now none of the containers are binded to the host hence are not actually running. they both are from the same port = 6379

##### 9. binding host and container port

![image-20210513201311009](C:\Users\ishit\AppData\Roaming\Typora\typora-user-images\image-20210513201311009.png)

```dockerfile
docker run -p6000:6379 redis

docker run -p6000:6379 -d redis //to run in detached mode
```

-p means port
6000 is the host port we are binding the container port to
6379 is the container port

we see  **0.0.0.0:6000->6379/tcp** which mean the containers port is binded to out laptops's 6000 port

**remember to bind the same container ports to different local host ports**

![image-20210513202007045](C:\Users\ishit\AppData\Roaming\Typora\typora-user-images\image-20210513202007045.png)

many different containers were created when we binded the ports

if we connect the containers to the same port we'll receive and error: *port is already allocated*

![image-20210513202149313](C:\Users\ishit\AppData\Roaming\Typora\typora-user-images\image-20210513202149313.png)

we've binded the containers to local port!

![image-20210513202328267](C:\Users\ishit\AppData\Roaming\Typora\typora-user-images\image-20210513202328267.png)

converted both in detached mode:

![image-20210513202456856](C:\Users\ishit\AppData\Roaming\Typora\typora-user-images\image-20210513202456856.png)



##### NOTE:

docker run - create a new container from a image
run makes changes or specifies all the changes or additions you want to make to a container before even making it, i.e associate with the image 
and once the image is converted to a container you can't edit the changes but make a new container to update it

docker start - you are working with containers and not images



### debugging containers ( commands for troubleshooting)

```
exec -it, logs (debugging the container)
```

##### 1. docker logs 

```dockerfile
docker logs *container id/name of the container*
```

if there is any problem like can't connect to the container you can go the logs of the container

![image-20210513204540520](C:\Users\ishit\AppData\Roaming\Typora\typora-user-images\image-20210513204540520.png)

you can either use the name or the container id to get the logs

every container when made gets a random name 

##### 2.  --name *name given*

```dockerfile
docker run -d -p6002:6379 --name redis-old redis:4.0
```

![image-20210513222415671](C:\Users\ishit\AppData\Roaming\Typora\typora-user-images\image-20210513222415671.png)

you can name your container whatever you want to maybe differentiate from other versions of the same container or for easy use.

everytime you change a port, or rename or connect to a new local host port. a new container is created. hence the new container id

##### 3. docker exec -it

-it means *interactive terminal*

we use exec whenever we want to change terminate the terminal or maybe direct a terminal inside, check the log file or config file or print out environmental variables

```dockerfile
docker exec -it *container id* /bin/bash
```

the cursor changes which means you are inside the container as a root user

![image-20210513223955717](C:\Users\ishit\AppData\Roaming\Typora\typora-user-images\image-20210513223955717.png)

###### ls 

to look what's inside the file you are currently in

###### pwd 

print which directory you are in

###### cd (change directories)

navigate to different directories
cd / (takes you to the home directory)

env (environmental directory) - to look if everything is set correctly

###### exit

to exit the terminal

![image-20210513224317649](C:\Users\ishit\AppData\Roaming\Typora\typora-user-images\image-20210513224317649.png)

remember you can use the name too...

since most of the container images are based on light weight linux distributions, don't have much linux commands and applications involved hence limited. 



### project:

