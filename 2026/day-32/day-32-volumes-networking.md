Task 1: The Problem
Run a Postgres or MySQL container
Create some data inside it (a table, a few rows — anything)
Stop and remove the container
Run a new one — is your data still there?
Write what happened and why.

 docker run -d --name my_db -e MYSQL_ROOT_PASSWORD=MYPASSWORD mysql:latest
Unable to find image 'mysql:latest' locally
latest: Pulling from library/mysql
74a8e4bbd9fe: Pull complete
357926362d31: Pull complete
f3702ac323ca: Pull complete
658630c937c6: Pull complete
ab1b8ea72826: Pull complete
61941d436e88: Pull complete
c89a19cdad3b: Pull complete
00af5f73db53: Pull complete
8314ff001dec: Pull complete
4a629f1008ff: Pull complete
Digest: sha256:e5dc14f6e01c3e577e669337d2855c6d1561b30d8ef2c592e63e4e8a9a52650a
Status: Downloaded newer image for mysql:latest
3df5b94044f2b3e0704f0bcc5a991d8ce331a561cab75d34d1de5fd3046f9fae
parnav@DESKTOP-2PGT0AC:~$ docker images
REPOSITORY   TAG       IMAGE ID       CREATED      SIZE
mysql        latest    8458fdfc578c   7 days ago   922MB
parnav@DESKTOP-2PGT0AC:~$ docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS          PORTS                 NAMES
3df5b94044f2   mysql:latest   "docker-entrypoint.s…"   38 seconds ago   Up 37 seconds   3306/tcp, 33060/tcp   my_db
parnav@DESKTOP-2PGT0AC:~$ docker exac -d 3df

mysql> show database
    -> show database;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'database
show database' at line 1
mysql> show DATABASE:
    -> show DATABASE;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'DATABASE:
show DATABASE' at line 1
mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
4 rows in set (0.010 sec)

mysql> CREATE DATABASE mydatapri;
Query OK, 1 row affected (0.017 sec)

mysql> SHOW DATABASES;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| mydatapri          |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
5 rows in set (0.001 sec)

mysql> CREATE TABLE mydatapri (column1 datatype, column2 datatype);
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'datatype, column2 datatype)' at line 

mysql> USE mydatapri;
Database changed
mysql> CREATE TABLE mydatapri (     id INT PRIMARY KEY,     name VARCHAR(50),     age INT,     course VARCHAR(20) );
Query OK, 0 rows affected (0.021 sec)

mysql> DESCRIBE mydatapri
    -> DESCRIBE mydatapri;
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near 'DESCRIBE mydatapri' at line 2
mysql> CREATE TABLE student (     id INT PRIMARY KEY,     name VARCHAR(50),     age INT,     course VARCHAR(20) );
Query OK, 0 rows affected (0.019 sec)

mysql> DESCRIBE students;
ERROR 1146 (42S02): Table 'mydatapri.students' doesn't exist
mysql> exit
Bye
bash-5.1# exit
exit
parnav@DESKTOP-2PGT0AC:~$


<<<<<<<<<<<<<<<<<<<<<<>>>>>>>>>no data i here everthing i gone <<<<<<<<<<<<<<<<<>>>>>>>>>>>>>>>>>

Task 2: Named Volumes
Create a named volume
Run the same database container, but this time attach the volume to it
Add some data, stop and remove the container
Run a brand new container with the same volume
Is the data still there?
Verify: docker volume ls, docker volume inspect

parnav@DESKTOP-2PGT0AC:~/mysqldata$ docker run -d -v /home/parnav/mysqldata:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=root mysql:latest
f4f6b8d85d4f740960a238a88882c60584752e27c3c60c95f719f09839ca43b5
parnav@DESKTOP-2PGT0AC:~/mysqldata$
parnav@DESKTOP-2PGT0AC:~/mysqldata$ docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS          PORTS                 NAMES
f4f6b8d85d4f   mysql:latest   "docker-entrypoint.s…"   27 seconds ago   Up 26 seconds   3306/tcp, 33060/tcp   thirsty_hodgkin
parnav@DESKTOP-2PGT0AC:~/mysqldata$ docker exec -it f4f bash
bash-5.1# ls
afs  boot  docker-entrypoint-initdb.d  home  lib64  mnt  proc  run   srv  tmp  var
bin  dev   etc                         lib   media  opt  root  sbin  sys  usr
bash-5.1# cd /var/lib/mysql
bash-5.1# ls
'#ib_16384_0.dblwr'   binlog.000001   ca.pem            ibdata1                 performance_schema   undo_001
'#ib_16384_1.dblwr'   binlog.000002   client-cert.pem   ibtmp1                  private_key.pem      undo_002
'#innodb_redo'        binlog.000003   client-key.pem    mysql                   public_key.pem       you
'#innodb_temp'        binlog.index    hay               mysql.ibd               server-cert.pem
 are                  budy            how               mysql.sock              server-key.pem
 auto.cnf             ca-key.pem      ib_buffer_pool    mysql_upgrade_history   sys
bash-5.1# mkdir teacher
bash-5.1# ls
'#ib_16384_0.dblwr'   binlog.000001   ca.pem            ibdata1                 performance_schema   teacher
'#ib_16384_1.dblwr'   binlog.000002   client-cert.pem   ibtmp1                  private_key.pem      undo_001
'#innodb_redo'        binlog.000003   client-key.pem    mysql                   public_key.pem       undo_002
'#innodb_temp'        binlog.index    hay               mysql.ibd               server-cert.pem      you
 are                  budy            how               mysql.sock              server-key.pem
 auto.cnf             ca-key.pem      ib_buffer_pool    mysql_upgrade_history   sys
bash-5.1# exit
exit
parnav@DESKTOP-2PGT0AC:~/mysqldata$ ls
'#ib_16384_0.dblwr'   binlog.000001   ca.pem            ibdata1                 performance_schema   teacher
'#ib_16384_1.dblwr'   binlog.000002   client-cert.pem   ibtmp1                  private_key.pem      undo_001
'#innodb_redo'        binlog.000003   client-key.pem    mysql                   public_key.pem       undo_002
'#innodb_temp'        binlog.index    hay               mysql.ibd               server-cert.pem      you
 are                  budy            how               mysql.sock              server-key.pem
 auto.cnf             ca-key.pem      ib_buffer_pool    mysql_upgrade_history   sys
parnav@DESKTOP-2PGT0AC:~/mysqldata$ docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED         STATUS         PORTS                 NAMES
f4f6b8d85d4f   mysql:latest   "docker-entrypoint.s…"   2 minutes ago   Up 2 minutes   3306/tcp, 33060/tcp   thirsty_hodgkin
parnav@DESKTOP-2PGT0AC:~/mysqldata$ docker stop f4f && docker rm f4f
f4f
f4f
parnav@DESKTOP-2PGT0AC:~/mysqldata$

>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>task 3<<<<<<<<<<<<<<<<<<<<<<<<<<>>>>>>>>>>>>>>>>>>>>>>>>>>

Task 3: Bind Mounts
Create a folder on your host machine with an index.html file
Run an Nginx container and bind mount your folder to the Nginx web directory
Access the page in your browser
Edit the index.html on your host — refresh the browser
Write in your notes: What is the difference between a named volume and a bind mount?



parnav@DESKTOP-2PGT0AC:~/mysqldata$ docker run -d -v mysqldata:/usr/share/nginx/html --network host -p 80:80 --name my
nginx nginx:latest
WARNING: Published ports are discarded when using host network mode
10988672f0175ddf984860487f752ca33a61ea68d54d132b309de19e4d2fc236
parnav@DESKTOP-2PGT0AC:~/mysqldata$ docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS         PORTS     NAMES
10988672f017   nginx:latest   "/docker-entrypoint.…"   10 seconds ago   Up 9 seconds             mynginx
parnav@DESKTOP-2PGT0AC:~/mysqldata$ docker network inspect host
[
    {
        "Name": "host",
        "Id": "71c9a3a818f9282f5debefb2f9ab98520c363929068c172178f67ef339c35521",
        "Created": "2026-02-26T05:16:11.918507524Z",
        "Scope": "local",
        "Driver": "host",
        "EnableIPv4": true,
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": null,
            "Config": null
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {
            "10988672f0175ddf984860487f752ca33a61ea68d54d132b309de19e4d2fc236": {
                "Name": "mynginx",
                "EndpointID": "9a99f6c01e6792b36088144381ceb0afa2e55b30abc070a12ca7ec3e699093ba",
                "MacAddress": "",
                "IPv4Address": "",
                "IPv6Address": ""
            }
        },
        "Options": {},
        "Labels": {}
    }
]
parnav@DESKTOP-2PGT0AC:~/mysqldata$ ls
'#ib_16384_0.dblwr'   binlog.000001   ca.pem            ibdata1                 performance_schema   teacher
'#ib_16384_1.dblwr'   binlog.000002   client-cert.pem   index.html              private_key.pem      undo_001
'#innodb_redo'        binlog.000003   client-key.pem    mysql                   public_key.pem       undo_002
'#innodb_temp'        binlog.index    hay               mysql.ibd               server-cert.pem      you
 are                  budy            how               mysql.sock              server-key.pem
 auto.cnf             ca-key.pem      ib_buffer_pool    mysql_upgrade_history   sys
parnav@DESKTOP-2PGT0AC:~/mysqldata$ docker exec -it mynginx bash
root@DESKTOP-2PGT0AC:/# ls
bin   dev                  docker-entrypoint.sh  home  lib64  mnt  proc  run   srv  tmp  var
boot  docker-entrypoint.d  etc                   lib   media  opt  root  sbin  sys  usr
root@DESKTOP-2PGT0AC:/# grep -i *index.html
^C
root@DESKTOP-2PGT0AC:/# grep -R "index.html" /
^C
root@DESKTOP-2PGT0AC:/# find / -name index.html
/usr/share/nginx/html/index.html
find: '/proc/29/task/29/fdinfo': Permission denied
find: '/proc/29/map_files': Permission denied
find: '/proc/29/fdinfo': Permission denied
find: '/proc/30/task/30/fdinfo': Permission denied
find: '/proc/30/map_files': Permission denied
find: '/proc/30/fdinfo': Permission denied
find: '/proc/31/task/31/fdinfo': Permission denied
find: '/proc/31/map_files': Permission denied
find: '/proc/31/fdinfo': Permission denied
find: '/proc/32/task/32/fdinfo': Permission denied
find: '/proc/32/map_files': Permission denied
find: '/proc/32/fdinfo': Permission denied
find: '/proc/33/task/33/fdinfo': Permission denied
find: '/proc/33/map_files': Permission denied
find: '/proc/33/fdinfo': Permission denied
find: '/proc/34/task/34/fdinfo': Permission denied
find: '/proc/34/map_files': Permission denied
find: '/proc/34/fdinfo': Permission denied
find: '/proc/35/task/35/fdinfo': Permission denied
find: '/proc/35/map_files': Permission denied
find: '/proc/35/fdinfo': Permission denied
find: '/proc/36/task/36/fdinfo': Permission denied
find: '/proc/36/map_files': Permission denied
find: '/proc/36/fdinfo': Permission denied
root@DESKTOP-2PGT0AC:/# cat /usr/share/nginx/html/index.html
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
root@DESKTOP-2PGT0AC:/# exit
exit
parnav@DESKTOP-2PGT0AC:~/mysqldata$ docker ps
CONTAINER ID   IMAGE          COMMAND                  CREATED          STATUS          PORTS     NAMES
10988672f017   nginx:latest   "/docker-entrypoint.…"   13 minutes ago   Up 13 minutes             mynginx
parnav@DESKTOP-2PGT0AC:~/mysqldata$ docker cp index.html mynginx:/usr/share/nginx/html/
Successfully copied 4.1kB to mynginx:/usr/share/nginx/html/
parnav@DESKTOP-2PGT0AC:~/mysqldata$ docker run -d -v mysqldata:/usr/share/nginx/html --network host -p 80:80 --name mynginx nginx:latest

>>>>>>>>>>it changes directly on web page <<<<<<<<<<<<,>>>>>>>>>>>>


Task 4: Docker Networking Basics

List all Docker networks on your machine
parnav@DESKTOP-2PGT0AC:~/mysqldata$ docker network ls
NETWORK ID     NAME      DRIVER    SCOPE
a51d2b9f0b55   bankapp   bridge    local
e0b84c239054   bridge    bridge    local
71c9a3a818f9   host      host      local
34ec780d6575   none      null      local
parnav@DESKTOP-2PGT0AC:~/mysqldata$

Inspect the default bridge network
parnav@DESKTOP-2PGT0AC:~/mysqldata$ docker network inspect bankapp
[
    {
        "Name": "bankapp",
        "Id": "a51d2b9f0b5563225c4875ac3a07de5bbb89b245945397f6f3077d48eb913187",
        "Created": "2026-02-26T05:31:53.987066336Z",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv4": true,
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": {},
            "Config": [
                {
                    "Subnet": "172.18.0.0/16",
                    "Gateway": "172.18.0.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {},
        "Options": {},
        "Labels": {}
    }
]
parnav@DESKTOP-2PGT0AC:~/mysqldata$

Run two containers on the default bridge — can they ping each other by name?
parnav@DESKTOP-2PGT0AC:~/mysqldata$ docker run -dit --network bankapp --name container2 ubuntu:latest
1367372827afe5349f8bd7ae7d24d6c2397743245a43aa0932897b99b32674d5
parnav@DESKTOP-2PGT0AC:~/mysqldata$ docker run -dit --network bankapp --name container1 ubuntu:latest
d1b436527ddd213d6e576deb9befdc5d243ab49b6df0c703f39d332ada6701f2
parnav@DESKTOP-2PGT0AC:~/mysqldata$ docker ps
CONTAINER ID   IMAGE           COMMAND       CREATED          STATUS          PORTS     NAMES
d1b436527ddd   ubuntu:latest   "/bin/bash"   5 seconds ago    Up 5 seconds              container1
1367372827af   ubuntu:latest   "/bin/bash"   15 seconds ago   Up 14 seconds             container2
parnav@DESKTOP-2PGT0AC:~/mysqldata$ docker exec -it container1 bash
root@d1b436527ddd:/# ping container2
bash: ping: command not found
root@d1b436527ddd:/# apt update
Get:1 http://security.ubuntu.com/ubuntu noble-security InRelease [126 kB]
Get:2 http://archive.ubuntu.com/ubuntu noble InRelease [256 kB]
Get:3 http://archive.ubuntu.com/ubuntu noble-updates InRelease [126 kB]
Get:4 http://archive.ubuntu.com/ubuntu noble-backports InRelease [126 kB]
Get:5 http://security.ubuntu.com/ubuntu noble-security/main amd64 Packages [1883 kB]
Get:6 http://archive.ubuntu.com/ubuntu noble/multiverse amd64 Packages [331 kB]
Get:7 http://archive.ubuntu.com/ubuntu noble/main amd64 Packages [1808 kB]
Get:8 http://archive.ubuntu.com/ubuntu noble/restricted amd64 Packages [117 kB]
Get:9 http://archive.ubuntu.com/ubuntu noble/universe amd64 Packages [19.3 MB]
Get:10 http://security.ubuntu.com/ubuntu noble-security/restricted amd64 Packages [3262 kB]
Get:11 http://security.ubuntu.com/ubuntu noble-security/multiverse amd64 Packages [34.8 kB]
Get:12 http://security.ubuntu.com/ubuntu noble-security/universe amd64 Packages [1242 kB]
Get:13 http://archive.ubuntu.com/ubuntu noble-updates/main amd64 Packages [2276 kB]
Get:14 http://archive.ubuntu.com/ubuntu noble-updates/restricted amd64 Packages [3471 kB]
Get:15 http://archive.ubuntu.com/ubuntu noble-updates/universe amd64 Packages [2017 kB]
Get:16 http://archive.ubuntu.com/ubuntu noble-updates/multiverse amd64 Packages [38.1 kB]
Get:17 http://archive.ubuntu.com/ubuntu noble-backports/universe amd64 Packages [34.6 kB]
Get:18 http://archive.ubuntu.com/ubuntu noble-backports/main amd64 Packages [49.5 kB]
Fetched 36.5 MB in 11s (3300 kB/s)
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
4 packages can be upgraded. Run 'apt list --upgradable' to see them.
root@d1b436527ddd:/# ping container2
bash: ping: command not found
root@d1b436527ddd:/# apt install iputils-ping -y
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  libcap2-bin libpam-cap
The following NEW packages will be installed:
  iputils-ping libcap2-bin libpam-cap
0 upgraded, 3 newly installed, 0 to remove and 4 not upgraded.
Need to get 91.2 kB of archives.
After this operation, 322 kB of additional disk space will be used.
Get:1 http://archive.ubuntu.com/ubuntu noble-updates/main amd64 libcap2-bin amd64 1:2.66-5ubuntu2.2 [34.2 kB]
Get:2 http://archive.ubuntu.com/ubuntu noble-updates/main amd64 iputils-ping amd64 3:20240117-1ubuntu0.1 [44.6 kB]
Get:3 http://archive.ubuntu.com/ubuntu noble-updates/main amd64 libpam-cap amd64 1:2.66-5ubuntu2.2 [12.5 kB]
Fetched 91.2 kB in 2s (48.0 kB/s)
debconf: delaying package configuration, since apt-utils is not installed
Selecting previously unselected package libcap2-bin.
(Reading database ... 4381 files and directories currently installed.)
Preparing to unpack .../libcap2-bin_1%3a2.66-5ubuntu2.2_amd64.deb ...
Unpacking libcap2-bin (1:2.66-5ubuntu2.2) ...
Selecting previously unselected package iputils-ping.
Preparing to unpack .../iputils-ping_3%3a20240117-1ubuntu0.1_amd64.deb ...
Unpacking iputils-ping (3:20240117-1ubuntu0.1) ...
Selecting previously unselected package libpam-cap:amd64.
Preparing to unpack .../libpam-cap_1%3a2.66-5ubuntu2.2_amd64.deb ...
Unpacking libpam-cap:amd64 (1:2.66-5ubuntu2.2) ...
Setting up libcap2-bin (1:2.66-5ubuntu2.2) ...
Setting up libpam-cap:amd64 (1:2.66-5ubuntu2.2) ...
debconf: unable to initialize frontend: Dialog
debconf: (No usable dialog-like program is installed, so the dialog based frontend cannot be used. at /usr/share/perl5/Debconf/FrontEnd/Dialog.pm line 79.)
debconf: falling back to frontend: Readline
debconf: unable to initialize frontend: Readline
debconf: (Can't locate Term/ReadLine.pm in @INC (you may need to install the Term::ReadLine module) (@INC entries checked: /etc/perl /usr/local/lib/x86_64-linux-gnu/perl/5.38.2 /usr/local/share/perl/5.38.2 /usr/lib/x86_64-linux-gnu/perl5/5.38 /usr/share/perl5 /usr/lib/x86_64-linux-gnu/perl-base /usr/lib/x86_64-linux-gnu/perl/5.38 /usr/share/perl/5.38 /usr/local/lib/site_perl) at /usr/share/perl5/Debconf/FrontEnd/Readline.pm line 8.)
debconf: falling back to frontend: Teletype
Setting up iputils-ping (3:20240117-1ubuntu0.1) ...
root@d1b436527ddd:/# ping container2
PING container2 (172.18.0.2) 56(84) bytes of data.
64 bytes from container2.bankapp (172.18.0.2): icmp_seq=1 ttl=64 time=0.397 ms
64 bytes from container2.bankapp (172.18.0.2): icmp_seq=2 ttl=64 time=0.125 ms
64 bytes from container2.bankapp (172.18.0.2): icmp_seq=3 ttl=64 time=0.049 ms
64 bytes from container2.bankapp (172.18.0.2): icmp_seq=4 ttl=64 time=0.052 ms
^C
--- container2 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3036ms
rtt min/avg/max/mdev = 0.049/0.155/0.397/0.142 ms
root@d1b436527ddd:/#
Run two containers on the default bridge — can they ping each other by IP?
parnav@DESKTOP-2PGT0AC:~/mysqldata$ docker exec -it container1 bash
root@d1b436527ddd:/# ping 1367
PING 1367 (0.0.5.87) 56(84) bytes of data.
^C
--- 1367 ping statistics ---
11 packets transmitted, 0 received, 100% packet loss, time 10241ms

root@d1b436527ddd:/# ping 1367372827af
PING 1367372827af (172.18.0.2) 56(84) bytes of data.
64 bytes from container2.bankapp (172.18.0.2): icmp_seq=1 ttl=64 time=0.194 ms
64 bytes from container2.bankapp (172.18.0.2): icmp_seq=2 ttl=64 time=0.062 ms
64 bytes from container2.bankapp (172.18.0.2): icmp_seq=3 ttl=64 time=0.045 ms
64 bytes from container2.bankapp (172.18.0.2): icmp_seq=4 ttl=64 time=0.057 ms
^C
--- 1367372827af ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3041ms
rtt min/avg/max/mdev = 0.045/0.089/0.194/0.060 ms
root@d1b436527ddd:/#


ask 5: Custom Networks
Create a custom bridge network called my-app-net
Run two containers on my-app-net
Can they ping each other by name now?
Write in your notes: Why does custom networking allow name-based communication but the default bridge doesn't?

done 


Task 6: Put It Together
Create a custom network
Run a database container (MySQL/Postgres) on that network with a volume for data
Run an app container (use any image) on the same network
Verify the app container can reach the database by container name

done 
