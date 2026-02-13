Task 1: Your First Script
Create a file hello.sh
Add the shebang line #!/bin/bash at the top
Print Hello, DevOps! using echo
Make it executable and run it

parnav@DESKTOP-2PGT0AC:~$ vi hello.sh
parnav@DESKTOP-2PGT0AC:~$ chmod 764 hello.sh
parnav@DESKTOP-2PGT0AC:~$ ls
app.log  company_data.txt  hello.sh  notes.txt
parnav@DESKTOP-2PGT0AC:~$ ./hello.sh
 Hello, DevOps!
parnav@DESKTOP-2PGT0AC:~$

if we remove the shebang  it will take default shell  to eecute /bin/sh
What happens?
OS tries to execute file
No shebang → no interpreter defined
System uses default shell (usually /bin/sh)

Task 2: Variables
Create variables.sh with:
A variable for your NAME
A variable for your ROLE (e.g., "DevOps Engineer")
Print: Hello, I am <NAME> and I am a <ROLE>
Try using single quotes vs double quotes — what's the difference?

parnav@DESKTOP-2PGT0AC:~$ vi variables.sh
parnav@DESKTOP-2PGT0AC:~$ chmod 764 variables.sh
parnav@DESKTOP-2PGT0AC:~$ ls
app.log  company_data.txt  hello.sh  notes.txt  variables.sh
parnav@DESKTOP-2PGT0AC:~$ ./variables.sh
./variables.sh: line 3: NAMEParnav: command not found
./variables.sh: line 4: ROLEDevOps Engineer: command not found
Hello , I am DESKTOP-2PGT0AC and i am a
parnav@DESKTOP-2PGT0AC:~$ vi variables.sh
parnav@DESKTOP-2PGT0AC:~$ ls
app.log  company_data.txt  hello.sh  notes.txt  variables.sh
parnav@DESKTOP-2PGT0AC:~$ ./variables.sh
Hello , I am Parnav and i am a DevOps Engineer
parnav@DESKTOP-2PGT0AC:~$

Try using single quotes vs double quotes — what's the difference?
#!/bin/bash

NAME="Parnav"
ROLE="DevOps Engineer"
echo 'Hello , I am $NAME and i am a $ROLE'

not it is not able to featch name and role  variable 


Task 3: User Input with read
Create greet.sh that:
Asks the user for their name using read
Asks for their favourite tool
Prints: Hello <name>, your favourite tool is <tool>

parnav@DESKTOP-2PGT0AC:~$ ./greet.sh
Name=enter your name parnav
Tool=enter your favourite tool Techno
Hello , your favourite tool is
parnav@DESKTOP-2PGT0AC:~$ vi greet.sh
parnav@DESKTOP-2PGT0AC:~$ ./greet.sh
enter your name parnav
enter your favourite tool jenkins
Hello parnav, your favourite tool is
parnav@DESKTOP-2PGT0AC:~$ vi greet.sh
parnav@DESKTOP-2PGT0AC:~$ ./greet.sh
enter your name parnav
enter your favourite tool dev
Hello parnav, your favourite tool is dev
parnav@DESKTOP-2PGT0AC:~$

Task 4: If-Else Conditions
Create check_number.sh that:

Takes a number using read
Prints whether it is positive, negative, or zero
Create file_check.sh that::

parnav@DESKTOP-2PGT0AC:~$ ./selfcheck.sh
give us a no 7
posetive
parnav@DESKTOP-2PGT0AC:~$ ./selfcheck.sh
give us a no -9
./selfcheck.sh: line 12: echonegative: command not found
parnav@DESKTOP-2PGT0AC:~$ vi selfcheck.sh
parnav@DESKTOP-2PGT0AC:~$ ./selfcheck.sh
give us a no -9
negative

Asks for a filename
Checks if the file exists using -f
Prints appropriate message

parnav@DESKTOP-2PGT0AC:~$ touch file_check.sh
parnav@DESKTOP-2PGT0AC:~$ vi file_check.sh
parnav@DESKTOP-2PGT0AC:~$ chmod 764 file_check.sh
parnav@DESKTOP-2PGT0AC:~$ ./file_check.sh
./file_check.sh: line 4: get: command not found
enter a file name
file exixt
parnav@DESKTOP-2PGT0AC:~$ ./file_check.sh
./file_check.sh: line 4: get: command not found
enter a file name check_number.sh
./file_check.sh: line 8: [: missing `]'
file do not exist
parnav@DESKTOP-2PGT0AC:~$ ./file_check.sh
./file_check.sh: line 4: get: command not found
enter a file name app.log
./file_check.sh: line 8: [: missing `]'
file do not exist
parnav@DESKTOP-2PGT0AC:~$ vi file_check.sh
parnav@DESKTOP-2PGT0AC:~$ ./file_check.sh
enter a file name app.log
./file_check.sh: line 7: [: missing `]'
file do not exist
parnav@DESKTOP-2PGT0AC:~$ vi file_check.sh
parnav@DESKTOP-2PGT0AC:~$ ./file_check.sh
enter a file name app.log
file exixt
parnav@DESKTOP-2PGT0AC:~$


Task 5: Combine It All
Create server_check.sh that:

Stores a service name in a variable (e.g., nginx, sshd)
Asks the user: "Do you want to check the status? (y/n)"
If y — runs systemctl status <service> and prints whether it's active or not
If n — prints "Skipped."
ubuntu@ip-172-31-21-44:~$ vi server_check.sh
ubuntu@ip-172-31-21-44:~$ chmod 764 server_check.sh
ubuntu@ip-172-31-21-44:~$ ./server_check.sh
enter a service name to check status ssh
Do you want to check the status? (y/n)y
./server_check.sh: line 13: unexpected EOF while looking for matching `"'
ubuntu@ip-172-31-21-44:~$ vi server_check.sh
ubuntu@ip-172-31-21-44:~$ ./server_check.sh
enter a service name to check status ssh
Do you want to check the status? (y/n)y
./server_check.sh: line 13: unexpected EOF while looking for matching `"'
ubuntu@ip-172-31-21-44:~$ vi server_check.sh
ubuntu@ip-172-31-21-44:~$ ./server_check.sh
enter a service name to check status ssh
Do you want to check the status? (y/n)y
./server_check.sh: line 7: [: y: unary operator expected
./server_check.sh: line 11: [: y: unary operator expected
ubuntu@ip-172-31-21-44:~$ vi server_check.sh
ubuntu@ip-172-31-21-44:~$ vi server_check.sh
ubuntu@ip-172-31-21-44:~$ ./server_check.sh
enter a service name to check status ssh
Do you want to check the status? (y/n)y
     Active: active (running) since Fri 2026-02-13 09:20:05 UTC; 12min ago
ubuntu@ip-172-31-21-44:~$
ubuntu@ip-172-31-21-44:~$ ./server_check.sh
enter a service name to check status ssh
Do you want to check the status? (y/n)y
     Active: active (running) since Fri 2026-02-13 09:20:05 UTC; 12min ago
ubuntu@ip-172-31-21-44:~$./server_check.sh
enter a service name to check status ssh
Do you want to check the status? (y/n)n
skipped
ubuntu@ip-172-31-21-44:~$ 




