Task 1: What is Docker?

Research and write short notes on:
What is a container and why do we need them?
1 Why Do We Need Containers?

What is a Container?
A container is a lightweight, standalone, executable package that includes:
Application code
Runtime
System tools
Libraries
Dependencies
It runs consistently across environments (Dev → Test → Prod).
👉 Problem it solves:
“It works on my machine but not on server.”
Containers ensure environment consistency.

2️⃣ Why Do We Need Containers?
Before containers:
pps were installed directly on OS
ependency conflicts were common
Scaling was difficult
Deployment was slow
Containers solve
Isolation
Portability
Faster deployment
Better resource usage
Containers vs Virtual Machines — what's the real difference?
What is the Docker architecture? (daemon, client, images, containers, registry)
Draw or describe the Docker architecture in your own words.
<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>
Task 2: Install Docker
Install Docker on your machine (or use a cloud instance)

sudo apt install docker.io
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
docker.io is already the newest version (28.2.2-0ubuntu1~24.04.1).
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.

Verify the installation
ubuntu@ip-172-31-21-241:~$ docker --version
Docker version 28.2.2, build 28.2.2-0ubuntu1~24.04.1

>>>>>>>>>>>>>>>>Run the hello-world container<<<<<<<<<<<<<<<

docker run -it hello-world

ubuntu@ip-172-31-21-241:~$ docker run -it hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
17eec7bbc9d7: Pull complete
Digest: sha256:ef54e839ef541993b4e87f25e752f7cf4238fa55f017957c2eb44077083d7a6a
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/




Read the output carefully — it explains what just happened
<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<<>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>

Task 3: Run Real Containers
Run an Nginx container and access it in your browser
ubuntu@ip-172-31-21-241:~$docker run -d --name my_nginx nginx
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
0c8d55a45c0d: Pull complete
46bf3a120c8e: Pull complete
4f4efe02d542: Pull complete
7b6cb8ccac7b: Pull complete
f73400a233fd: Pull complete
47cd406a84ef: Pull complete
bae5a1799a80: Pull complete
Digest: sha256:341bf0f3ce6c5277d6002cf6e1fb0319fa4252add24ab6a0e262e0056d313208
Status: Downloaded newer image for nginx:latest
5b14e36292f63f6f9060286caf1c2fdc7459f2acb1425c8526d1f62c8bbaefb7
Run an Ubuntu container in interactive mode — explore it like a mini Linux machine
ubuntu@ip-172-31-21-241:~$ docker images
REPOSITORY    TAG       IMAGE ID       CREATED        SIZE
ubuntu        latest    bbdabce66f1b   11 days ago    78.1MB
nginx         latest    5cdef4ac3335   2 weeks ago    161MB
hello-world   latest    1b44b5a3e06a   6 months ago   10.1kB
ubuntu@ip-172-31-21-241:~$ docker run -it ubuntu
root@8dd0c1feaa67:/#

List all running containers
doker 
List all containers (including stopped ones)
docker ps -a 

Stop and remove a container
docker stop my_nginx &&  docker rm my_nginx



Task 4: Explore
Run a container in detached mode — what's different?
docker run -d nginx

Give a container a custom name
docker run -it -name my_nginx nginx 

Map a port from the container to your host
docker run -d -p 8080:80 --name my-nginx nginx

Check logs of a running container
docker logs <container_name>

Run a command inside a running container
docker exac -it <container name >