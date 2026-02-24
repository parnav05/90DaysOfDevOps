Task 1: Your First Dockerfile
Create a folder called my-first-image
Inside it, create a Dockerfile that:
Uses ubuntu as the base image
Installs curl
Sets a default command to print "Hello from my custom image!"
Build the image and tag it my-ubuntu:v1
Run a container from your image
Verify: The message prints on docker run

answer 
done.
 ---> Removed intermediate container f8a9b26212cd
 ---> ca5b61e523d8
Step 3/3 : CMD ["echo","Hello from my custom image!"]
 ---> Running in 04883aa498a1
 ---> Removed intermediate container 04883aa498a1
 ---> b3f56a46d7fa
Successfully built b3f56a46d7fa
Successfully tagged my-ubuntu:v1
ubuntu@ip-172-31-21-241:~/my-first-image$ docker run -it my-ubuntu:v1
Hello from my custom image!





Task 2: Dockerfile Instructions
Create a new Dockerfile that uses all of these instructions:

FROM — base image
RUN — execute commands during build
COPY — copy files from host to image
WORKDIR — set working directory
EXPOSE — document the port
CMD — default command
Build and run it. Understand what each line does.

FROM python:latest (jamin kharidna )

WORKDIR /app  (naksha banwana )

COPY requirements.txt . (saman jama krna requirements )

RUN pip install -r requirements.txt (mistry ko bulana jo )

COPY . . (banki sara saman lana : bathrom ka eloctronics kitchen )

EXPOSE 5000 (gate lagwana )

CMD ["python", "app.py"] (rhna start karna )








Task 3: CMD vs ENTRYPOINT
Create an image with CMD ["echo", "hello"] — run it, then run it with a custom command. What happens?
Create an image with ENTRYPOINT ["echo"] — run it, then run it with additional arguments. What happens?
Write in your notes: When would you use CMD vs ENTRYPOINT?
cmd 
Step 5/6 : EXPOSE 80
 ---> Running in c8c2059ce45c
 ---> Removed intermediate container c8c2059ce45c
 ---> d993de72a72f
Step 6/6 : CMD ["echo","hay budy This my container "]
 ---> Running in 7523a382f67f
 ---> Removed intermediate container 7523a382f67f
 ---> 87c4c5bdd693
Successfully built 87c4c5bdd693
Successfully tagged tera_data:latest
ubuntu@ip-172-31-21-241:~/my-first-image/task3$ docker run -it 87c
hay budy This my container

entrypoint 

Step 5/6 : EXPOSE 80
 ---> Running in 451e3c69ee51
 ---> Removed intermediate container 451e3c69ee51
 ---> 8eb076a019f4
Step 6/6 : ENTRYPOINT ["echo","hay budy This my container "]
 ---> Running in 9bc280754bcf
 ---> Removed intermediate container 9bc280754bcf
 ---> ab07d4c7830e
Successfully built ab07d4c7830e
Successfully tagged tera_data:latest
ubuntu@ip-172-31-21-241:~/my-first-image/task3$ docker run -it ab07
hay budy This my container
ubuntu@ip-172-31-21-241:~/my-first-image/task3$

Write in your notes: When would you use CMD vs ENTRYPOINT?
CMD vs ENTRYPOINT — When to Use
🔹 CMD (Default Command)
Kab use kare?
Jab tum container ko default behavior dena chahte ho
Jab tum chahte ho ki user command override kar sake
xample use case:
Run a Python app by default
Run a script, but allow user to change it
Example:
CMD ["python3", "app.py"]
👉 User override kar sakta hai:
docker run my-image python3 test.py
🔹 ENTRYPOINT (Fixed Command)
Kab use kare?
Jab tum container ko ek specific tool ya command banana chahte ho
Jab tum nahi chahte ki main command change ho
Example use case:
Container as a CLI tool (curl, ping, etc.)
Always run same binary
Example:
ENTRYPOINT ["curl"]
👉 Run:
docker run my-image google.com
👉 Actual run:
curl google.com




Task 4: Build a Simple Web App Image
Create a small static HTML file (index.html) with any content
Write a Dockerfile that:
Uses nginx:alpine as base
Copies your index.html to the Nginx web directory
Build and tag it my-website:v1
Run it with port mapping and access it in your browser

Step 1/4 : FROM nginx:alpine
 ---> b76de378d572
Step 2/4 : WORKDIR /app
 ---> Using cache
 ---> 10e61873d932
Step 3/4 : COPY index.html /usr/share/nginx/html
 ---> 61cbcc888d3f
Step 4/4 : EXPOSE 80
 ---> Running in 0340a55a9629
 ---> Removed intermediate container 0340a55a9629
 ---> 78e639be16a2
Successfully built 78e639be16a2
Successfully tagged my-website:v1
ubuntu@ip-172-31-21-241:~/my-first-image/task4$ docker run -d -p 80:80 78e
0a4184f95ba4d85c2a5a5728d7ef430b19490a0fa325b2c58a57790c1b674ef7
ubuntu@ip-172-31-21-241:~/my-first-image/task4$ docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS                                 NAMES
0a4184f95ba4   78e       "/docker-entrypoint.…"   7 seconds ago   Up 7 seconds   0.0.0.0:80->80/tcp, [::]:80->80/tcp   cranky_lamarr
ubuntu@ip-172-31-21-241:~/my-first-image/task4$




Task 5: .dockerignore
Create a .dockerignore file in one of your project folders
Add entries for: node_modules, .git, *.md, .env
Build the image — verify that ignored files are not included

CONTAINER ID   IMAGE       COMMAND                  CREATED              STATUS              PORTS                                         NAMES
cef4afc79d6a   my_app.py   "python app.py"          About a minute ago   Up About a minute   0.0.0.0:5000->5000/tcp, [::]:5000->5000/tcp   hopeful_allen
0a4184f95ba4   78e         "/docker-entrypoint.…"   21 minutes ago       Up 21 minutes       0.0.0.0:80->80/tcp, [::]:80->80/tcp           cranky_lamarr
ubuntu@ip-172-31-21-241:~/my-first-image/task2$ docker exec -it cef
docker: 'docker exec' requires at least 2 arguments

Usage:  docker exec [OPTIONS] CONTAINER COMMAND [ARG...]

See 'docker exec --help' for more information
ubuntu@ip-172-31-21-241:~/my-first-image/task2$ docker exec -it cef bash
root@cef4afc79d6a:/app# ls
Dockerfile  app.py  requirements.txt
root@cef4afc79d6a:/app#

.dockerignore file is not here 



Task 6: Build Optimization
Build an image, then change one line and rebuild — notice how Docker uses cache
Reorder your Dockerfile so that frequently changing lines come last
Write in your notes: Why does layer order matter for build speed?


Docker har instruction ko layer banata hai
👉 Agar change nahi hua → cache reuse karta hai
observation : 


jaha se  error aaya tha fir  file mai changes karne k bad ahi se suru ho jata hai 

