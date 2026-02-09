task 1 
Task 1: Create Files (10 minutes)
Create empty file devops.txt using touch
Create notes.txt with some content using cat or echo
Create script.sh using vim with content: echo "Hello DevOps"
Verify: ls -l to see permissions



ubuntu@ip-172-31-44-7:~$ cd /home
ubuntu@ip-172-31-44-7:/home$ ls
berlin  nairobi  professor  tokyo  ubuntu
ubuntu@ip-172-31-44-7:/home$ cd ubuntu/
ubuntu@ip-172-31-44-7:~$ ls
ubuntu@ip-172-31-44-7:~$ touch devops.txt
ubuntu@ip-172-31-44-7:~$ echo "hay how are you  i am parnav dev i am learning deops " >>notes.txt
ubuntu@ip-172-31-44-7:~$ vim script.sh
ubuntu@ip-172-31-44-7:~$ ls -lh
total 8.0K
-rw-rw-r-- 1 ubuntu ubuntu  0 Feb  9 11:34 devops.txt
-rw-rw-r-- 1 ubuntu ubuntu 54 Feb  9 11:35 notes.txt
-rw-rw-r-- 1 ubuntu ubuntu 21 Feb  9 11:36 script.sh
ubuntu@ip-172-31-44-7:~$ ^C

task 2 
Task 2: Read Files (10 minutes)
Read notes.txt using cat
View script.sh in vim read-only mode
Display first 5 lines of /etc/passwd using head
Display last 5 lines of /etc/passwd using tail

ubuntu@ip-172-31-44-7:~$ ^C
ubuntu@ip-172-31-44-7:~$ cat notes.txt
Command 'cat' not found, but there are 17 similar ones.
ubuntu@ip-172-31-44-7:~$ cat notes.txt
hay how are you  i am parnav dev i am learning deops
ubuntu@ip-172-31-44-7:~$ vi script.sh


ubuntu@ip-172-31-44-7:~$ vim -R script.sh
ubuntu@ip-172-31-44-7:~$
echo "hello devops  "
~
~
~

"script.sh" [readonly] 1L, 22B  

ubuntu@ip-172-31-44-7:~$ cat /etc/passwd | head -5
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync


ubuntu@ip-172-31-44-7:~$cat /etc/passwd | tail -5
ubuntu:x:1000:1000:Ubuntu:/home/ubuntu:/bin/bash
berlin:x:1002:1002::/home/berlin:/bin/sh
professor:x:1003:1003::/home/professor:/bin/sh
tokyo:x:1004:1004::/home/tokyo:/bin/sh
nairobi:x:1005:1006::/home/nairobi:/bin/sh
ubuntu@ip-172-31-44-7:~$


Task 3: Understand Permissions (10 minutes)
Format: rwxrwxrwx (owner-group-others)

r = read (4), w = write (2), x = execute (1)
Check your files: ls -l devops.txt notes.txt script.sh

Answer: What are current permissions? Who can read/write/execute?

ubuntu@ip-172-31-44-7:~$ sudo chmod 777 devops.txt
ubuntu@ip-172-31-44-7:~$ sudo chmod 777 devops.txt notes.txt
ubuntu@ip-172-31-44-7:~$ sudo chmod 777 devops.txt notes.txt script.sh
ubuntu@ip-172-31-44-7:~$ ls -l
total 8
-rwxrwxrwx 1 ubuntu ubuntu  0 Feb  9 11:34 devops.txt
-rwxrwxrwx 1 ubuntu ubuntu 54 Feb  9 11:35 notes.txt
-rwxrwxrwx 1 ubuntu ubuntu 22 Feb  9 11:40 script.sh
ubuntu@ip-172-31-44-7:~$ ^C

Task 4: Modify Permissions (20 minutes)
Make script.sh executable → run it with ./script.sh
Set devops.txt to read-only (remove write for all)
Set notes.txt to 640 (owner: rw, group: r, others: none)
Create directory project/ with permissions 755
Verify: ls -l after each change


ubuntu@ip-172-31-44-7:~$ sudo chmod 777 script.sh
ubuntu@ip-172-31-44-7:~$ ./script.sh
hello devops
ubuntu@ip-172-31-44-7:~$ sudo chmod 444 devops.txt
ubuntu@ip-172-31-44-7:~$ ls -l
total 8
-r--r--r-- 1 ubuntu ubuntu  0 Feb  9 11:34 devops.txt
-rwxrwxrwx 1 ubuntu ubuntu 54 Feb  9 11:35 notes.txt
-rwxrwxrwx 1 ubuntu ubuntu 22 Feb  9 11:40 script.sh
ubuntu@ip-172-31-44-7:~$ sudo chmod 640 notes.txt
ubuntu@ip-172-31-44-7:~$ ls -l
total 8
-r--r--r-- 1 ubuntu ubuntu  0 Feb  9 11:34 devops.txt
-rw-r----- 1 ubuntu ubuntu 54 Feb  9 11:35 notes.txt
-rwxrwxrwx 1 ubuntu ubuntu 22 Feb  9 11:40 script.sh
ubuntu@ip-172-31-44-7:~$ mkdir  project | chmod 755 project
chmod: cannot access 'project': No such file or directory
ubuntu@ip-172-31-44-7:~$ mkdir project | chmod 755 project
mkdir: cannot create directory ‘project’: File exists
ubuntu@ip-172-31-44-7:~$ mkdir project
mkdir: cannot create directory ‘project’: File exists
ubuntu@ip-172-31-44-7:~$ sudo chmod 755 project/
ubuntu@ip-172-31-44-7:~$ ls -l
total 12
-r--r--r-- 1 ubuntu ubuntu    0 Feb  9 11:34 devops.txt
-rw-r----- 1 ubuntu ubuntu   54 Feb  9 11:35 notes.txt
drwxr-xr-x 2 ubuntu ubuntu 4096 Feb  9 12:16 project
-rwxrwxrwx 1 ubuntu ubuntu   22 Feb  9 11:40 script.sh
ubuntu@ip-172-31-44-7:~$

Task 5: Test Permissions (10 minutes)
Try writing to a read-only file - what happens?
Try executing a file without execute permission
Document the error messages


gdj
~


-- INSERT -- W10: Warning: Changing a readonly file  
gdj
~

E45: 'readonly' option is set (add ! to override)   


ubuntu@ip-172-31-44-7:~$ vim test.sh
ubuntu@ip-172-31-44-7:~$ ./test.sh
-bash: ./test.sh: Permission denied
ubuntu@ip-172-31-44-7:~$
