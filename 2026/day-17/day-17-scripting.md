Tas For Loop
Create for_loop.sh that:
Loops through a list of 5 fruits and prints each one
Create count.sh that:
Prints numbers 1 to 10 using a for loop

ubuntu@ip-172-31-16-96:~/devopschallange$ vim for_loop.sh
ubuntu@ip-172-31-16-96:~/devopschallange$ ./for_loop.sh
apple
banana
mango
greaps
beet
ubuntu@ip-172-31-16-96:~/devopschallange$ vi count.sh
ubuntu@ip-172-31-16-96:~/devopschallange$ chmod 764 count.sh
ubuntu@ip-172-31-16-96:~/devopschallange$ ./count.sh
1
2
3
4
5
6
7
8
9
10

Task 2: While Loop
Create countdown.sh that:
Takes a number from the user
Counts down to 0 using a while loop
Prints "Done!" at the end

#!/bin/bash


read -p "Enter a no " lmt

while [ $lmt -ge 0 ]
do

        echo "$lmt"
        ((lmt--))
        sleep 1
done

echo "done "
~

Task 3: Command-Line Arguments
Create greet.sh that:

Accepts a name as $1
Prints Hello, <name>!
If no argument is passed, prints "Usage: ./greet.sh "
Create args_demo.sh that:

Prints total number of arguments ($#)
Prints all arguments ($@)
Prints the script name ($0)

ubuntu@ip-172-31-30-172:~$  vi args.demo.sh
#!/bin/bash



<<comment



Create args_demo.sh that:

Prints total number of arguments ($#)
Prints all arguments ($@)
Prints the script name ($0)

comment


echo "total no of arguments $#"
echo "all arguments $@"
echo "print scriptname $0"

~
~
"args.demo.sh" 21L, 243B         
ubuntu@ip-172-31-30-172:~$ chmod  764 args.demo.sh
ubuntu@ip-172-31-30-172:~$ ./args.demo.sh
total no of arguments 0
all arguments
print scriptname ./args.demo.sh
ubuntu@ip-172-31-30-172:~$ ./args.demo.sh parnav dev sakshi ranjit
total no of arguments 4
all arguments parnav dev sakshi ranjit
print scriptname ./args.demo.sh
ubuntu@ip-172-31-30-172:~$


Task 4: Install Packages via Script
Create install_packages.sh that:
Defines a list of packages: nginx, curl, wget
Loops through the list
Checks if each package is installed (use dpkg -s or rpm -q)
Installs it if missing, skips if already present
Prints status for each package

vi install_packages.sh

No VM guests are running outdated hypervisor (qemu) binaries on this host.
nginx installed ✅
curl already installed ✅
wget already installed ✅
ubuntu@ip-172-31-30-172:~$

Task 5: Error Handling
Create safe_script.sh that:
Uses set -e at the top (exit on error)
Tries to create a directory /tmp/devops-test
Tries to navigate into it
Creates a file inside
Uses || operator to print an error if any step fails

#!/usr/bin/env bash
set -e

DIR="/tmp/devops-test"
FILE="test.txt"

# Create directory
mkdir -p "$DIR" || {
  echo "[ERROR] Failed to create directory: $DIR" >&2
  exit 1
}
echo "[INFO] Directory ready: $DIR"

# Navigate into directory
cd "$DIR" || {
  echo "[ERROR] Failed to navigate to directory: $DIR" >&2
  exit 1
}
echo "[INFO] Navigated to: $DIR"

# Create file
touch "$FILE" || {
  echo "[ERROR] Failed to create file: $FILE" >&2
  exit 1
}
echo "[INFO] File created: $FILE"




