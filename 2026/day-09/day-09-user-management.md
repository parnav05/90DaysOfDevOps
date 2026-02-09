ubuntu@ip-172-31-44-7:~$ sudo useradd -m berlin
ubuntu@ip-172-31-44-7:~$ sudo useradd -m professor
ubuntu@ip-172-31-44-7:~$ sudo passwd berlin
New password:
Retype new password:
passwd: password updated successfully
ubuntu@ip-172-31-44-7:~$ sudo passwd professor
New password:
Retype new password:
passwd: password updated successfully
ubuntu@ip-172-31-44-7:~$ cd /home
ubuntu@ip-172-31-44-7:/home$ ls
berlin  professor  ubuntu
ubuntu@ip-172-31-44-7:/home$ sudo useradd -m tokyo
useradd: user 'tokyo' already exists
ubuntu@ip-172-31-44-7:/home$ sudo deluser -m tokyo
Unknown option: m
ubuntu@ip-172-31-44-7:/home$ sudo deluser testuser
fatal: The user `testuser' does not exist.
ubuntu@ip-172-31-44-7:/home$ sudo deluser --remove-home username
fatal: The user `username' does not exist.
ubuntu@ip-172-31-44-7:/home$ sudo deluser --remove-home tokyo
info: Looking for files to backup/remove ...
info: Removing crontab ...
info: Removing user `tokyo' ...
ubuntu@ip-172-31-44-7:/home$ ls
berlin  professor  ubuntu
ubuntu@ip-172-31-44-7:/home$ sudo useradd -m tokyo
ubuntu@ip-172-31-44-7:/home$ ls
berlin  professor  tokyo  ubuntu
ubuntu@ip-172-31-44-7:/home$ cat /etc/passwd
root:x:0:0:root:/root:/bin/bash
ubuntu:x:1000:1000:Ubuntu:/home/ubuntu:/bin/bash
berlin:x:1002:1002::/home/berlin:/bin/sh
professor:x:1003:1003::/home/professor:/bin/sh
tokyo:x:1004:1004::/home/tokyo:/bin/sh
ubuntu@ip-172-31-44-7:/home$

task 2 

ubuntu@ip-172-31-44-7:/opt$ cat /etc/group
ubuntu:x:1000:
berlin:x:1002:
professor:x:1003:
tokyo:x:1004:
developers:x:1001:tokyo,berlin
admins:x:1005:berlin,professor
nairobi:x:1006:
project-team:x:1007:nairobi,tokyo
ubuntu@ip-172-31-44-7:/opt$



Task 3: Assign to Groups (15 minutes)
Assign users:

tokyo → developers
berlin → developers + admins (both groups)
professor → admins
Verify: Use appropriate command to check group membership 

ubuntu@ip-172-31-44-7:/opt$ cat /etc/group
developers:x:1001:tokyo,berlin
admins:x:1005:berlin,professor

task 4 
ask 4: Shared Directory (20 minutes)
Create directory: /opt/dev-project
Set group owner to developers
Set permissions to 775 (rwxrwxr-x)
Test by creating files as tokyo and berlin
Verify: Check permissions and test file creation


ubuntu@ip-172-31-44-7:/opt$ sudo ls -lh /opt/
total 8.0K
drwxrwxr-x 2 root developers   4.0K Feb  9 09:37 dev-project
drwxrwxr-x 2 root project-team 4.0K Feb  9 10:13 team-workspace


Task 5: Team Workspace (20 minutes)
Create user nairobi with home directory
Create group project-team
Add nairobi and tokyo to project-team
Create /opt/team-workspace directory
Set group to project-team, permissions to 775
Test by creating file as nairobi

ubuntu:x:1000:1000:Ubuntu:/home/ubuntu:/bin/bash
berlin:x:1002:1002::/home/berlin:/bin/sh
professor:x:1003:1003::/home/professor:/bin/sh
tokyo:x:1004:1004::/home/tokyo:/bin/sh
nairobi:x:1005:1006::/home/nairobi:/bin/sh


ubuntu:x:1000:
berlin:x:1002:
professor:x:1003:
tokyo:x:1004:
developers:x:1001:tokyo,berlin
admins:x:1005:berlin,professor
nairobi:x:1006:
project-team:x:1007:nairobi,tokyo

ubuntu@ip-172-31-44-7:/opt$ls -lh
total 8.0K
drwxrwxr-x 2 root developers   4.0K Feb  9 09:37 dev-project
drwxrwxr-x 2 root project-team 4.0K Feb  9 10:13 team-workspace
ubuntu@ip-172-31-44-7:/opt$


drwxrwxr-x 2 root project-team 4.0K Feb  9 10:13 team-workspace
