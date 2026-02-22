Task 1: Docker Images
Pull the nginx, ubuntu, and alpine images from Docker Hub
docker pull nginx:latest
docker pull ubuntu:latest
docker pull alpine:latest

List all images on your machine — note the sizes
ubuntu@ip-172-31-21-241:~$ docker images
REPOSITORY    TAG       IMAGE ID       CREATED        SIZE
ubuntu        latest    bbdabce66f1b   12 days ago    78.1MB
nginx         latest    5cdef4ac3335   2 weeks ago    161MB
httpd         latest    d2825031e94c   2 weeks ago    117MB
alpine        latest    a40c03cbb81c   3 weeks ago    8.44MB
hello-world   latest    1b44b5a3e06a   6 months ago   10.1kB

Compare ubuntu vs alpine — why is one much smaller?
ubuntu        latest    bbdabce66f1b   12 days ago    78.1MB
alpine        latest    a40c03cbb81c   3 weeks ago    8.44MB

alpine is amaller 

Inspect an image — what information can you see?
ubuntu@ip-172-31-21-241:~$ docker inspect ubuntu
[
    {
        "Id": "sha256:bbdabce66f1b7dde0c081a6b4536d837cd81dd322dd8c99edd68860baf3b2db3",
        "RepoTags": [
            "ubuntu:latest"
        ],
        "RepoDigests": [
            "ubuntu@sha256:d1e2e92c075e5ca139d51a140fff46f84315c0fdce203eab2807c7e495eff4f9"
        ],
        "Parent": "",
        "Comment": "",
        "Created": "2026-02-10T16:49:57.226767398Z",
        "DockerVersion": "26.1.3",
        "Author": "",
        "Config": {
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
            ],
            "Cmd": [
                "/bin/bash"
            ],
            "Labels": {
                "org.opencontainers.image.ref.name": "ubuntu",
                "org.opencontainers.image.version": "24.04"
            }
        },
        "Architecture": "amd64",
        "Os": "linux",
        "Size": 78129634,
        "GraphDriver": {
            "Data": {
                "MergedDir": "/var/lib/docker/overlay2/59085f45e485616cb7e466f605681b18bd9e560fc3552b61ed5f4690fa76548b/merged",
                "UpperDir": "/var/lib/docker/overlay2/59085f45e485616cb7e466f605681b18bd9e560fc3552b61ed5f4690fa76548b/diff",
                "WorkDir": "/var/lib/docker/overlay2/59085f45e485616cb7e466f605681b18bd9e560fc3552b61ed5f4690fa76548b/work"
            },
            "Name": "overlay2"
        },
        "RootFS": {
            "Type": "layers",
            "Layers": [
                "sha256:efafae78d70c98626c521c246827389128e7d7ea442db31bc433934647f0c791"
            ]
        },
        "Metadata": {
            "LastTagTime": "0001-01-01T00:00:00Z"


Remove an image you no longer need
ubuntu@ip-172-31-21-241:~$ docker rmi ubuntu:latest
Untagged: ubuntu:latest
Untagged: ubuntu@sha256:d1e2e92c075e5ca139d51a140fff46f84315c0fdce203eab2807c7e495eff4f9
Deleted: sha256:bbdabce66f1b7dde0c081a6b4536d837cd81dd322dd8c99edd68860baf3b2db3
Deleted: sha256:efafae78d70c98626c521c246827389128e7d7ea442db31bc433934647f0c791
ubuntu@ip-172-31-21-241:~$ docker image
Usage:  docker image COMMAND



Task 2: Image Layers
Run docker image history nginx — what do you see?
ubuntu@ip-172-31-21-241:~$ docker image history nginx
IMAGE          CREATED       CREATED BY                                      SIZE      COMMENT
5cdef4ac3335   2 weeks ago   CMD ["nginx" "-g" "daemon off;"]                0B        buildkit.dockerfile.v0
<missing>      2 weeks ago   STOPSIGNAL SIGQUIT                              0B        buildkit.dockerfile.v0
<missing>      2 weeks ago   EXPOSE map[80/tcp:{}]                           0B        buildkit.dockerfile.v0
<missing>      2 weeks ago   ENTRYPOINT ["/docker-entrypoint.sh"]            0B        buildkit.dockerfile.v0
<missing>      2 weeks ago   COPY 30-tune-worker-processes.sh /docker-ent…   4.62kB    buildkit.dockerfile.v0
<missing>      2 weeks ago   COPY 20-envsubst-on-templates.sh /docker-ent…   3.02kB    buildkit.dockerfile.v0
<missing>      2 weeks ago   COPY 15-local-resolvers.envsh /docker-entryp…   389B      buildkit.dockerfile.v0
<missing>      2 weeks ago   COPY 10-listen-on-ipv6-by-default.sh /docker…   2.12kB    buildkit.dockerfile.v0
<missing>      2 weeks ago   COPY docker-entrypoint.sh / # buildkit          1.62kB    buildkit.dockerfile.v0
<missing>      2 weeks ago   RUN /bin/sh -c set -x     && groupadd --syst…   82.2MB    buildkit.dockerfile.v0
<missing>      2 weeks ago   ENV DYNPKG_RELEASE=1~trixie                     0B        buildkit.dockerfile.v0
<missing>      2 weeks ago   ENV PKG_RELEASE=1~trixie                        0B        buildkit.dockerfile.v0
<missing>      2 weeks ago   ENV ACME_VERSION=0.3.1                          0B        buildkit.dockerfile.v0
<missing>      2 weeks ago   ENV NJS_RELEASE=1~trixie                        0B        buildkit.dockerfile.v0
<missing>      2 weeks ago   ENV NJS_VERSION=0.9.5                           0B        buildkit.dockerfile.v0
<missing>      2 weeks ago   ENV NGINX_VERSION=1.29.5                        0B        buildkit.dockerfile.v0
<missing>      2 weeks ago   LABEL maintainer=NGINX Docker Maintainers <d…   0B        buildkit.dockerfile.v0
<missing>      2 weeks ago   # debian.sh --arch 'amd64' out/ 'trixie' '@1…   78.6MB    debuerreotype 0.17
ubuntu@ip-172-31-21-241:~$ 

Each line is a layer. Note how some layers show sizes and some show 0B
Packages install ho rahe hain
Files add ho rahe hain
Directories create ho rahi hain
Isliye iska size bada hai.

Metadata add karti hain
Configuration define karti hain
Koi file add/remove nahi hoti
Isliye size = 0B

Write in your notes: What are layers and why does Docker use them?
A layer is:

👉 A read-only filesystem change
👉 Created by each instruction in a Dockerfile
👉 Stacked on top of previous layers

Simple definition:
Docker image = stack of layers.
Example Dockerfile
FROM ubuntu
RUN apt update
RUN apt install nginx -y
COPY . /app
CMD ["nginx", "-g", "daemon off;"]
Yahan:
FROM ubuntu → Layer 1
RUN apt update → Layer 2
RUN install nginx → Layer 3
COPY → Layer 4
CMD → Layer 5
Each line = one layer.


why does Docker use them?
Docker uses layers for:
1️⃣ Reusability
If multiple images use:
FROM ubuntu
That base layer is reused.
No need to download again.
2️⃣ Faster Builds (Caching)
If nothing changes in a layer:
Docker reuses cached layer.
Example:
If only COPY changes,
Docker doesn’t reinstall nginx.
Huge CI/CD speed improvement 🚀
3️⃣ Less Storage Usage
Layers are shared.
If 5 containers use same image:
Base layers stored only once.
4️⃣ Faster Pulls
When pulling image:
Dcker downloads only missing layers.
Already downloaded layers are skipped.
5️⃣ Isolation
Each layer is immutable (cannot change).
When container runs:
Docker adds one more writable layer on top.
That’s called:
👉 Container layer
🔥 Important Conc



Task 3: Container Lifecycle
Practice the full lifecycle on one container:

Create a container (without starting it)
Start the container
Pause it and check status
Unpause it
Stop it
Restart it
Kill it
Remove it
Check docker ps -a after each step — observe the state changes.

ubuntu@ip-172-31-21-241:~$ docker start e42c
e42c
ubuntu@ip-172-31-21-241:~$ docker stop e42c
e42c
ubuntu@ip-172-31-21-241:~$ docker start e42c
e42c
ubuntu@ip-172-31-21-241:~$ docker pause nginx
Error response from daemon: No such container: nginx
ubuntu@ip-172-31-21-241:~$ docker pause e42c
e42c
ubuntu@ip-172-31-21-241:~$ docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED             STATUS                       PORTS                                     NAMES
e42cb0067853   nginx     "/docker-entrypoint.…"   8 minutes ago       Up About a minute (Paused)   0.0.0.0:7869->80/tcp, [::]:7869->80/tcp   dazzling_mayer
467f05e77056   httpd     "httpd-foreground"       About an hour ago   Up About an hour             0.0.0.0:80->80/tcp, [::]:80->80/tcp       laughing_varahamihira
ubuntu@ip-172-31-21-241:~$ docker unpause e42c
e42c
ubuntu@ip-172-31-21-241:~$ docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED             STATUS             PORTS                                     NAMES
e42cb0067853   nginx     "/docker-entrypoint.…"   9 minutes ago       Up 2 minutes       0.0.0.0:7869->80/tcp, [::]:7869->80/tcp   dazzling_mayer
467f05e77056   httpd     "httpd-foreground"       About an hour ago   Up About an hour   0.0.0.0:80->80/tcp, [::]:80->80/tcp       laughing_varahamihira
ubuntu@ip-172-31-21-241:~$ docker stop e42c
e42c
ubuntu@ip-172-31-21-241:~$ docker restart e42c
e42c
ubuntu@ip-172-31-21-241:~$ docker kill e42c
e42c
ubuntu@ip-172-31-21-241:~$ docker ps
CONTAINER ID   IMAGE     COMMAND              CREATED             STATUS             PORTS                                 NAMES
467f05e77056   httpd     "httpd-foreground"   About an hour ago   Up About an hour   0.0.0.0:80->80/tcp, [::]:80->80/tcp   laughing_varahamihira
ubuntu@ip-172-31-21-241:~$ docker remove httpd
Error response from daemon: No such container: httpd
ubuntu@ip-172-31-21-241:~$ ^C
ubuntu@ip-172-31-21-241:~$ ^C
ubuntu@ip-172-31-21-241:~$ docker remove 242c
Error response from daemon: No such container: 242c
ubuntu@ip-172-31-21-241:~$ docker remove e42c
e42c
ubuntu@ip-172-31-21-241:~$ docker ps
CONTAINER ID   IMAGE     COMMAND              CREATED             STATUS             PORTS                                 NAMES
467f05e77056   httpd     "httpd-foreground"   About an hour ago   Up About an hour   0.0.0.0:80->80/tcp, [::]:80->80/tcp   laughing_varahamihira



Task 4: Working with Running Containers
Run an Nginx container in detached mode
docker run -d -p 80:80 nginx

ubuntu@ip-172-31-21-241:~$ docker run -d -p 80:80 nginx
03747e0fc05a30c0aa44a5a70fe788197fdee9acb61e554136c1243cb79d6808
docker: Error response from daemon: failed to set up container networking: driver failed programming external connectivity on endpoint unruffled_murdock (62c6b7ebbfa6c3f94488b9db275a646f209626d4749898488f6577dd30a2bd31): Bind for 0.0.0.0:80 failed: port is already allocated

Run 'docker run --help' for more information
ubuntu@ip-172-31-21-241:~$ docker run -d -p 8086:8076 nginx
556d2185ccf72aaf57cf588a6ac72ae9afa91cecf9be1a4bbe6c703c516d64be
ubuntu@ip-172-31-21-241:~$


View its logs
ubuntu@ip-172-31-21-241:~$ docker logs 556
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2026/02/22 20:40:56 [notice] 1#1: using the "epoll" event method
2026/02/22 20:40:56 [notice] 1#1: nginx/1.29.5
2026/02/22 20:40:56 [notice] 1#1: built by gcc 14.2.0 (Debian 14.2.0-19)
2026/02/22 20:40:56 [notice] 1#1: OS: Linux 6.17.0-1007-aws
2026/02/22 20:40:56 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1048576:1048576
2026/02/22 20:40:56 [notice] 1#1: start worker processes
2026/02/22 20:40:56 [notice] 1#1: start worker process 30
2026/02/22 20:40:56 [notice] 1#1: start worker process 31
ubuntu@ip-172-31-21-241:~$

View real-time logs (follow mode)

Exec into the container and look around the filesystem
docker exac -it container id  bash 
Run a single command inside the container without entering it
Inspect the container — find its IP address, port mappings, and mounts
 "HostIp": "",
                        "HostPort": "8086"



Task 5: Cleanup
Stop all running containers in one command
docker stop $(docker ps -q)
Remove all stopped containers in one command
docker container prune 
Remove unused images
docker rmi image id 
Check how much disk space Docker is using

docker system df 