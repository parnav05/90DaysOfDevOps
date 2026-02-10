Task 1: Understanding Ownership (10 minutes)
Run ls -l in your home directory
Identify the owner and group columns
Check who owns your files
Format: -rw-r--r-- 1 owner group size date filename

Document: What's the difference between owner and group?

answer 
drwxr-x--- 4 ubuntu ubuntu 4096 Feb 10 07:08 ubuntu
d 
Symbol	Meaning
d	Directory
-	Normal file
l	Symbolic link
c	Character device
b	Block device
drwxr-x--- 4 ubuntu ubuntu 4096 Feb 10 07:08 ubuntu
 rwx >>user 
 r → read (ls kar sakta hai)
 w → write (create/delete files)
 x → execute (cd kar sakta hai) 
drwxr-x--- 4 ubuntu ubuntu 4096 Feb 10 07:08 ubuntu
    r-x>>group 
drwxr-x--- 4 ubuntu ubuntu 4096 Feb 10 07:08 ubuntu
       --- >>other 
drwxr-x--- 4 ubuntu ubuntu 4096   Feb 10 07:08        ubuntu
             user | group  |size | Last Modified Time |  name of file 


Task 2: Basic chown Operations (20 minutes)
Create file devops-file.txt
Check current owner: ls -l devops-file.txt
Change owner to tokyo (create user if needed)
Change owner to berlin
Verify the changes
Try:

sudo chown tokyo devops-file.txt

answer >>>>>>>>>>>>>>>>>>>>>>>>
ubuntu@ip-172-31-16-85:/home$ sudo useradd -m tokyo
ubuntu@ip-172-31-16-85:/home$ sudo useradd -m berlin
ubuntu@ip-172-31-16-85:/home$ echo "hay buddy parctice daily " >>devops-file.txt
-bash: devops-file.txt: Permission denied
ubuntu@ip-172-31-16-85:/home$ sudo echo "hay buddy parctice daily " >>devops-file.txt
-bash: devops-file.txt: Permission denied
ubuntu@ip-172-31-16-85:/home$ sudo echo "hay buddy parctice daily " >>devops-file.txt
-bash: devops-file.txt: Permission denied
ubuntu@ip-172-31-16-85:/home$ sudo echo "hay buddy parctice daily " >> devops-file.txt
-bash: devops-file.txt: Permission denied
ubuntu@ip-172-31-16-85:/home$ ls
berlin  tokyo  ubuntu
ubuntu@ip-172-31-16-85:/home$ cd ubuntu/
ubuntu@ip-172-31-16-85:~$ sudo echo "hay buddy parctice daily " >> devops-file.txt
ubuntu@ip-172-31-16-85:~$ chown tokyo devops-file.txt
chown: changing ownership of 'devops-file.txt': Operation not permitted
ubuntu@ip-172-31-16-85:~$ sudo chown tokyo devops-file.txt
ubuntu@ip-172-31-16-85:~$ ls -l
total 4
-rw-rw-r-- 1 tokyo ubuntu 26 Feb 10 10:24 devops-file.txt
ubuntu@ip-172-31-16-85:~$ chown berlin devops-file.txt
chown: changing ownership of 'devops-file.txt': Operation not permitted
ubuntu@ip-172-31-16-85:~$ sudo chown berlin devops-file.txt
ubuntu@ip-172-31-16-85:~$ ls -l
total 4
-rw-rw-r-- 1 berlin ubuntu 26 Feb 10 10:24 devops-file.txt
ubuntu@ip-172-31-16-85:~$




Task 3: Basic chgrp Operations (15 minutes)
Create file team-notes.txt
Check current group: ls -l team-notes.txt
Create group: sudo groupadd heist-team
Change file group to heist-team
Verify the change


answer >>>>>>>>>>>>>>>>>>>
ubuntu@ip-172-31-16-85:~$ echo "hay buddy " >> team-notes.txt
ubuntu@ip-172-31-16-85:~$ ls -l
total 8
-rw-rw-r-- 1 ubuntu ubuntu  0 Feb 10 10:28 ''$'\033''[200~'
-rw-rw-r-- 1 berlin ubuntu 26 Feb 10 10:24  devops-file.txt
-rw-rw-r-- 1 ubuntu ubuntu 11 Feb 10 10:29  team-notes.txt
ubuntu@ip-172-31-16-85:~$ sudo groupadd ^[[200~heist-team
^[[201~groupadd: failure while writing changes to /etc/group
ubuntu@ip-172-31-16-85:~$ sudo groupadd heist-team
ubuntu@ip-172-31-16-85:~$ sudo chgrp heist-team
chgrp: missing operand after ‘heist-team’
Try 'chgrp --help' for more information.
ubuntu@ip-172-31-16-85:~$ sudo chgrp heist-team team-notes.txt
ubuntu@ip-172-31-16-85:~$ ls -l
total 8
-rw-rw-r-- 1 ubuntu ubuntu      0 Feb 10 10:28 ''$'\033''[200~'
-rw-rw-r-- 1 berlin ubuntu     26 Feb 10 10:24  devops-file.txt
-rw-rw-r-- 1 ubuntu heist-team 11 Feb 10 10:29  team-notes.txt
ubuntu@ip-172-31-16-85:~$



Task 4: Combined Owner & Group Change (15 minutes)
Using chown you can change both owner and group together:

Create file project-config.yaml
Change owner to professor AND group to heist-team (one command)
Create directory app-logs/
Change its owner to berlin and group to heist-team
Syntax: sudo chown owner:group filename

ubuntu@ip-172-31-16-85:~$ touch project-config.yaml
Command 'touch' not found, did you mean:
  command 'touch' from deb coreutils (9.4-3ubuntu6.1)
  command 'ktouch' from deb ktouch (4:23.08.4-0ubuntu1)
Try: sudo apt install <deb name>
ubuntu@ip-172-31-16-85:~$ touch project-config.yaml
ubuntu@ip-172-31-16-85:~$ sudo useradd -m professor
ubuntu@ip-172-31-16-85:~$ sudo chown professo:heist-team project-config.yaml
ubuntu@ip-172-31-16-85:~$ ls -l
total 8
-rw-rw-r-- 1 ubuntu    ubuntu      0 Feb 10 10:28 ''$'\033''[200~'
-rw-rw-r-- 1 berlin    ubuntu     26 Feb 10 10:24  devops-file.txt
-rw-rw-r-- 1 professor heist-team  0 Feb 10 10:34  project-config.yaml
-rw-rw-r-- 1 ubuntu    heist-team 11 Feb 10 10:29  team-notes.txt
ubuntu@ip-172-31-16-85:~$ mkdir app_log
ubuntu@ip-172-31-16-85:~$ sudo chown berlin : heist-team app_log/
chown: cannot access ':': No such file or directory
chown: cannot access 'heist-team': No such file or directory
ubuntu@ip-172-31-16-85:~$ ls -l
total 12
-rw-rw-r-- 1 ubuntu    ubuntu        0 Feb 10 10:28 ''$'\033''[200~'
drwxrwxr-x 2 berlin    ubuntu     4096 Feb 10 10:39  app_log
-rw-rw-r-- 1 berlin    ubuntu       26 Feb 10 10:24  devops-file.txt
-rw-rw-r-- 1 professor heist-team    0 Feb 10 10:34  project-config.yaml
-rw-rw-r-- 1 ubuntu    heist-team   11 Feb 10 10:29  team-notes.txt
ubuntu@ip-172-31-16-85:~$ sudo chown berlin : heist-team app_log/
chown: cannot access ':': No such file or directory
chown: cannot access 'heist-team': No such file or directory
ubuntu@ip-172-31-16-85:~$ sudo chown berlin : heist-team app_log/
chown: cannot access ':': No such file or directory
chown: cannot access 'heist-team': No such file or directory
ubuntu@ip-172-31-16-85:~$ sudo chown berlin:heist-team app_log
ubuntu@ip-172-31-16-85:~$ ls -l
total 12
-rw-rw-r-- 1 ubuntu    ubuntu        0 Feb 10 10:28 ''$'\033''[200~'
drwxrwxr-x 2 berlin    heist-team 4096 Feb 10 10:39  app_log
-rw-rw-r-- 1 berlin    ubuntu       26 Feb 10 10:24  devops-file.txt
-rw-rw-r-- 1 professor heist-team    0 Feb 10 10:34  project-config.yaml
-rw-rw-r-- 1 ubuntu    heist-team   11 Feb 10 10:29  team-notes.txt
ubuntu@ip-172-31-16-85:~$ ^C
ubuntu@ip-172-31-16-85:~$





Task 5: Recursive Ownership (20 minutes)
Create directory structure:

mkdir -p heist-project/vault
mkdir -p heist-project/plans
touch heist-project/vault/gold.txt
touch heist-project/plans/strategy.conf
Create group planners: sudo groupadd planners

Change ownership of entire heist-project/ directory:

Owner: professor
Group: planners
Use recursive flag (-R)
Verify all files and subdirectories changed: ls -lR heist-project/
ans wer <<<<<<<>>>>>>>
ubuntu@ip-172-31-16-85:~$ mkdir -p heist-project/vault
ubuntu@ip-172-31-16-85:~$ ls
''$'\033''[200~'   devops-file.txt   project-config.yaml
 app_log           heist-project     team-notes.txt
ubuntu@ip-172-31-16-85:~$ mkdir -p heist-project/vault
ubuntu@ip-172-31-16-85:~$ touch heist-project/vault/gold.txt
ubuntu@ip-172-31-16-85:~$ rm heist-project/vault/gold.txt
ubuntu@ip-172-31-16-85:~$ ls
''$'\033''[200~'   devops-file.txt   project-config.yaml
 app_log           heist-project     team-notes.txt
ubuntu@ip-172-31-16-85:~$ touch heist-project/vault/gold.txt
ubuntu@ip-172-31-16-85:~$ touch heist-project/plans/strategy.txt
touch: cannot touch 'heist-project/plans/strategy.txt': No such file or directory
ubuntu@ip-172-31-16-85:~$ ls heist-project/
vault
ubuntu@ip-172-31-16-85:~$ mkdir -p heist-project/plans
ubuntu@ip-172-31-16-85:~$ touch heist-project/plans/strategy.txt
ubuntu@ip-172-31-16-85:~$ sudo groupadd planners
ubuntu@ip-172-31-16-85:~$ chown -R professor:planners heist-project/
chown: changing ownership of 'heist-project/vault/gold.txt': Operation not permitted
chown: changing ownership of 'heist-project/vault': Operation not permitted
chown: changing ownership of 'heist-project/plans/strategy.txt': Operation not permitted
chown: changing ownership of 'heist-project/plans': Operation not permitted
chown: changing ownership of 'heist-project/': Operation not permitted
ubuntu@ip-172-31-16-85:~$ ls -l
total 16
-rw-rw-r-- 1 ubuntu    ubuntu        0 Feb 10 10:28 ''$'\033''[200~'
drwxrwxr-x 2 berlin    heist-team 4096 Feb 10 10:39  app_log
-rw-rw-r-- 1 berlin    ubuntu       26 Feb 10 10:24  devops-file.txt
drwxrwxr-x 4 ubuntu    ubuntu     4096 Feb 10 10:51  heist-project
-rw-rw-r-- 1 professor heist-team    0 Feb 10 10:34  project-config.yaml
-rw-rw-r-- 1 ubuntu    heist-team   11 Feb 10 10:29  team-notes.txt
ubuntu@ip-172-31-16-85:~$ sudo chown -R professor:planners heist-project/
ubuntu@ip-172-31-16-85:~$ ls -l
total 16
-rw-rw-r-- 1 ubuntu    ubuntu        0 Feb 10 10:28 ''$'\033''[200~'
drwxrwxr-x 2 berlin    heist-team 4096 Feb 10 10:39  app_log
-rw-rw-r-- 1 berlin    ubuntu       26 Feb 10 10:24  devops-file.txt
drwxrwxr-x 4 professor planners   4096 Feb 10 10:51  heist-project
-rw-rw-r-- 1 professor heist-team    0 Feb 10 10:34  project-config.yaml
-rw-rw-r-- 1 ubuntu    heist-team   11 Feb 10 10:29  team-notes.txt
ubuntu@ip-172-31-16-85:~$ cd  heist-project/
ubuntu@ip-172-31-16-85:~/heist-project$ ls
plans  vault
ubuntu@ip-172-31-16-85:~/heist-project$ ls -l
total 8
drwxrwxr-x 2 professor planners 4096 Feb 10 10:52 plans
drwxrwxr-x 2 professor planners 4096 Feb 10 10:50 vault
ubuntu@ip-172-31-16-85:~/heist-project$




Task 6: Practice Challenge (20 minutes)
Create users: tokyo, berlin, nairobi (if not already created)

Create groups: vault-team, tech-team

Create directory: bank-heist/

Create 3 files inside:

touch bank-heist/access-codes.txt
touch bank-heist/blueprints.pdf
touch bank-heist/escape-plan.txt
Set different ownership:

access-codes.txt → owner: tokyo, group: vault-team
blueprints.pdf → owner: berlin, group: tech-team
escape-plan.txt → owner: nairobi, group: vault-team
Verify: ls -l bank-heist/

answer<<<<<<<<<<<<<<<<<<>>>>>>>>>>>>>>>>>>

ubuntu@ip-172-31-16-85:~/heist-project$sudo useradd -m nairobi
ubuntu@ip-172-31-16-85:~/heist-project$ sudo groupadd vault-team
ubuntu@ip-172-31-16-85:~/heist-project$ sudo groupadd tech-team
ubuntu@ip-172-31-16-85:~/heist-project$ cd ..
ubuntu@ip-172-31-16-85:~$ ls -l
total 16
-rw-rw-r-- 1 ubuntu    ubuntu        0 Feb 10 10:28 ''$'\033''[200~'
drwxrwxr-x 2 berlin    heist-team 4096 Feb 10 10:39  app_log
-rw-rw-r-- 1 berlin    ubuntu       26 Feb 10 10:24  devops-file.txt
drwxrwxr-x 4 professor planners   4096 Feb 10 10:51  heist-project
-rw-rw-r-- 1 professor heist-team    0 Feb 10 10:34  project-config.yaml
-rw-rw-r-- 1 ubuntu    heist-team   11 Feb 10 10:29  team-notes.txt
ubuntu@ip-172-31-16-85:~$ mkdir bank-heist
ubuntu@ip-172-31-16-85:~$ touch bank-heist/access-codes.txt
ubuntu@ip-172-31-16-85:~$ touch bank-heist/blueprints.pdf
ubuntu@ip-172-31-16-85:~$ touch bank-heist/escape-plan.txt
ubuntu@ip-172-31-16-85:~$ sudo chown tokyo:vault-team /bank-heist/acc^C
ubuntu@ip-172-31-16-85:~$ ssudo chown tokyo:vault-team bank-heist/access-codes.txt
Command 'sudo' not found, did you mean:
  command 'sudo' from deb sudo (1.9.15p5-3ubuntu5.24.04.1)
  command 'sudo' from deb sudo-ldap (1.9.15p5-3ubuntu5.24.04.1)
Try: sudo apt install <deb name>
ubuntu@ip-172-31-16-85:~$ sudo chown tokyo:vault-team bank-heist/access-codes.txt
Command 'sudo' not found, did you mean:
  command 'sudo' from deb sudo (1.9.15p5-3ubuntu5.24.04.1)
  command 'sudo' from deb sudo-ldap (1.9.15p5-3ubuntu5.24.04.1)
Try: sudo apt install <deb name>
ubuntu@ip-172-31-16-85:~$ sudo chown tokyo:vault-team bank-heist/access-codes.txt
ubuntu@ip-172-31-16-85:~$ sudo chown berlin:tech-team bank-heist/blueprints.pdf
ubuntu@ip-172-31-16-85:~$ sudo chown n:tech-team bank-heist/blueprints.pdf
nairobi  news     nobody
ubuntu@ip-172-31-16-85:~$ sudo chown nairobi:vault-team bank-heist/esc
chown: cannot access 'bank-heist/esc': No such file or directory
ubuntu@ip-172-31-16-85:~$ sudo chown nairobi:vault-team bank-heist/escape-plan.txt
ubuntu@ip-172-31-16-85:~$ ls -l bank-heist/
total 0
-rw-rw-r-- 1 tokyo   vault-team 0 Feb 10 11:02 access-codes.txt
-rw-rw-r-- 1 berlin  tech-team  0 Feb 10 11:02 blueprints.pdf
-rw-rw-r-- 1 nairobi vault-team 0 Feb 10 11:02 escape-plan.txt
ubuntu@ip-172-31-16