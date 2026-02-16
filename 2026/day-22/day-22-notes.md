Task 1: Install and Configure Git
Verify Git is installed on your machine
Set up your Git identity — name and email
Verify your configuration


ubuntu@ip-172-31-30-172:~$ git version
git version 2.43.0

ubuntu@ip-172-31-30-172:~/git_github$ git config user.name "parnav"
ubuntu@ip-172-31-30-172:~/git_github$ git config user.mail "parnavdev05@gamil.com"
ubuntu@ip-172-31-30-172:~/git_github$ git log
ubuntu@ip-172-31-30-172:~/git_github$ git config --list
core.repositoryformatversion=0
core.filemode=true
core.bare=false
core.logallrefupdates=true
user.name=parnav
user.mail=parnavdev05@gamil.com


Task 2: Create Your Git Project
Create a new folder called devops-git-practice
Initialize it as a Git repository
Check the status — read and understand what Git is telling you
Explore the hidden .git/ directory — look at what's inside

ubuntu@ip-172-31-30-172:~$ mkdir devops-git-practice
ubuntu@ip-172-31-30-172:~/devops-git-practice$ git init
hint: Using 'master' as the name for the initial branch. This default branch name
hint: is subject to change. To configure the initial branch name to use in all
hint: of your new repositories, which will suppress this warning, call:
hint:
hint:   git config --global init.defaultBranch <name>
hint:
hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
hint: 'development'. The just-created branch can be renamed via this command:
hint:
hint:   git branch -m <name>
Initialized empty Git repository in /home/ubuntu/devops-git-practice/.git/

ubuntu@ip-172-31-30-172:~/devops-git-practice$ git status
On branch master

No commits yet

nothing to commit (create/copy files and use "git add" to track)

ubuntu@ip-172-31-30-172:~/devops-git-practice$ ls -la
total 12
drwxrwxr-x 3 ubuntu ubuntu 4096 Feb 16 19:47 .
drwxr-x--- 6 ubuntu ubuntu 4096 Feb 16 19:46 ..
drwxrwxr-x 7 ubuntu ubuntu 4096 Feb 16 19:47 .git
ubuntu@ip-172-31-30-172:~/devops-git-practice$ cd .git/
ubuntu@ip-172-31-30-172:~/devops-git-practice/.git$ ls
HEAD  branches  config  description  hooks  info  objects  refs

Task 3: Create Your Git Commands Reference
Create a file called git-commands.md inside the repo
Add the Git commands you've used so far, organized by category:
Setup & Config
Basic Workflow
Viewing Changes
For each command, write:
What it does (1 line)
An example of how to use it

ubuntu@ip-172-31-30-172:~/devops-git-practice/.git$history >> history >> git-commands.md
ubuntu@ip-172-31-30-172:~/devops-git-practice/.git$ cat git-commands.md
    1  vi countdown.sh
    2  chmod 764 countdown.sh
    3  ./countdown.sh
    4  vi countdown.sh
    5  ./countdown.sh
    6  vi countdown.sh
    7  ./countdown.sh
    8  vi countdown.sh
    9  ls
   10  cd git_github/
   11  git init
   12  git config user.name "parnav"
   13  git config user.mail "parnavdev05@gamil.com"
   14  git log
   15  git status
   16  touch file1.txt file2.txt file3.txt
   17  ls
   18  git status
   19  git config --list
   20  mkdir devops-git-practice
   21  mkdir devops-git-practice
   22  rm -r devops-git-practice/
   23  cd ..
   24  mkdir devops-git-practice
   25  git init
   26  git status
   27  rm-rf .git
   28  ls -la
   29  rm -rf .git
   30  ls
   31  git status
   32  cd devops-git-practice/
   33  ls
   34  git init
   35  git status
   36  cd .git
   37  ls -l
   38  ls -la
   39  cd .git/
   40  ls
   41  history >> history >> git-commands.md
ubuntu@ip-172-31-30-172:~/devops-git-practice/.git$

Task 4: Stage and Commit
Stage your file
Check what's staged
Commit with a meaningful message
View your commit history


ubuntu@ip-172-31-30-172:~/devops-git-practice$ mkdir h^C
ubuntu@ip-172-31-30-172:~/devops-git-practice$ git ststus
git: 'ststus' is not a git command. See 'git --help'.

The most similar command is
        status
ubuntu@ip-172-31-30-172:~/devops-git-practice$ touch file1.txt file2.txt file3.txt file.txt
ubuntu@ip-172-31-30-172:~/devops-git-practice$ ls
file.txt  file1.txt  file2.txt  file3.txt
ubuntu@ip-172-31-30-172:~/devops-git-practice$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        file.txt
        file1.txt
        file2.txt
        file3.txt

nothing added to commit but untracked files present (use "git add" to track)
ubuntu@ip-172-31-30-172:~/devops-git-practice$ git add file.txt
ubuntu@ip-172-31-30-172:~/devops-git-practice$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   file.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        file1.txt
        file2.txt
        file3.txt

ubuntu@ip-172-31-30-172:~/devops-git-practice$ git commit -m " file.txt"
[master (root-commit) 454ae68]  file.txt
 Committer: Ubuntu <ubuntu@ip-172-31-30-172.us-west-2.compute.internal>
Your name and email address were configured automatically based
on your username and hostname. Please check that they are accurate.
You can suppress this message by setting them explicitly. Run the
following command and follow the instructions in your editor to edit
your configuration file:

    git config --global --edit

After doing this, you may fix the identity used for this commit with:

    git commit --amend --reset-author

 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 file.txt
ubuntu@ip-172-31-30-172:~/devops-git-practice$ git log
commit 454ae682e9f6e38111a12fd10f9df6b974c4b6ef (HEAD -> master)
Author: Ubuntu <ubuntu@ip-172-31-30-172.us-west-2.compute.internal>
Date:   Mon Feb 16 20:02:33 2026 +0000

     file.txt
ubuntu@ip-172-31-30-172:~/devops-git-practice$ git config


Task 5: Make More Changes and Build History
Edit git-commands.md — add more commands as you discover them
Check what changed since your last commit
Stage and commit again with a different, descriptive message
Repeat this process at least 3 times so you have multiple commits in your history
View the full history in a compact format


nothing added to commit but untracked files present (use "git add" to track)
ubuntu@ip-172-31-30-172:~/devops-git-practice$ git add file.txt
ubuntu@ip-172-31-30-172:~/devops-git-practice$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   file.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        file1.txt
        file2.txt
        file3.txt

ubuntu@ip-172-31-30-172:~/devops-git-practice$ git commit -m " file.txt"
[master (root-commit) 454ae68]  file.txt
 Committer: Ubuntu <ubuntu@ip-172-31-30-172.us-west-2.compute.internal>
Your name and email address were configured automatically based
on your username and hostname. Please check that they are accurate.
You can suppress this message by setting them explicitly. Run the
following command and follow the instructions in your editor to edit
your configuration file:

    git config --global --edit

After doing this, you may fix the identity used for this commit with:

    git commit --amend --reset-author

 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 file.txt
ubuntu@ip-172-31-30-172:~/devops-git-practice$ git log
commit 454ae682e9f6e38111a12fd10f9df6b974c4b6ef (HEAD -> master)
Author: Ubuntu <ubuntu@ip-172-31-30-172.us-west-2.compute.internal>
Date:   Mon Feb 16 20:02:33 2026 +0000

     file.txt
ubuntu@ip-172-31-30-172:~/devops-git-practice$ touch git-commands.md
ubuntu@ip-172-31-30-172:~/devops-git-practice$ git add git-commands.md
ubuntu@ip-172-31-30-172:~/devops-git-practice$ git commit -m git-commands.md
[master 16eb177] git-commands.md
 Committer: Ubuntu <ubuntu@ip-172-31-30-172.us-west-2.compute.internal>
Your name and email address were configured automatically based
on your username and hostname. Please check that they are accurate.
You can suppress this message by setting them explicitly. Run the
following command and follow the instructions in your editor to edit
your configuration file:

    git config --global --edit

After doing this, you may fix the identity used for this commit with:

    git commit --amend --reset-author

 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 git-commands.md
ubuntu@ip-172-31-30-172:~/devops-git-practice$ git log
commit 16eb177a3b0c4a706b01a824da2d6efb646fa23a (HEAD -> master)
Author: Ubuntu <ubuntu@ip-172-31-30-172.us-west-2.compute.internal>
Date:   Mon Feb 16 20:07:28 2026 +0000

    git-commands.md

commit 454ae682e9f6e38111a12fd10f9df6b974c4b6ef
Author: Ubuntu <ubuntu@ip-172-31-30-172.us-west-2.compute.internal>
Date:   Mon Feb 16 20:02:33 2026 +0000

     file.txt
ubuntu@ip-172-31-30-172:~/devops-git-practice$ git config user.name "parnav"
ubuntu@ip-172-31-30-172:~/devops-git-practice$ git config user.email "parnavdev@gmail.com"
ubuntu@ip-172-31-30-172:~/devops-git-practice$ git log
commit 16eb177a3b0c4a706b01a824da2d6efb646fa23a (HEAD -> master)
Author: Ubuntu <ubuntu@ip-172-31-30-172.us-west-2.compute.internal>
Date:   Mon Feb 16 20:07:28 2026 +0000

    git-commands.md

commit 454ae682e9f6e38111a12fd10f9df6b974c4b6ef
Author: Ubuntu <ubuntu@ip-172-31-30-172.us-west-2.compute.internal>
Date:   Mon Feb 16 20:02:33 2026 +0000

     file.txt

ubuntu@ip-172-31-30-172:~/devops-git-practice$ git commit --amend --author "parnav <parnavdevo5.gmail.com> "
[master f214946] git-commands.md
 Author: parnav <parnavdevo5.gmail.com>
 Date: Mon Feb 16 20:07:28 2026 +0000
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 git-commands.md
ubuntu@ip-172-31-30-172:~/devops-git-practice$ git log
commit f2149467ad36eb3549996d495cfd92f57f04e282 (HEAD -> master)
Author: parnav <parnavdevo5.gmail.com>
Date:   Mon Feb 16 20:07:28 2026 +0000

    git-commands.md

commit 454ae682e9f6e38111a12fd10f9df6b974c4b6ef
Author: Ubuntu <ubuntu@ip-172-31-30-172.us-west-2.compute.internal>
Date:   Mon Feb 16 20:02:33 2026 +0000

     file.txt
ubuntu@ip-172-31-30-172:~/devops-git-practice$ git commit --amend --author "parnav <parnavdevo5.gmail.com> "
[master bef475d] git-commands.md
 Author: parnav <parnavdevo5.gmail.com>
 Date: Mon Feb 16 20:07:28 2026 +0000
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 git-commands.md
ubuntu@ip-172-31-30-172:~/devops-git-practice$ git log
commit bef475d39582cf11c96d2e5fabfe9eb32babb5c8 (HEAD -> master)
Author: parnav <parnavdevo5.gmail.com>
Date:   Mon Feb 16 20:07:28 2026 +0000

    git-commands.md

commit 454ae682e9f6e38111a12fd10f9df6b974c4b6ef
Author: Ubuntu <ubuntu@ip-172-31-30-172.us-west-2.compute.internal>
Date:   Mon Feb 16 20:02:33 2026 +0000

     file.txt
ubuntu@ip-172-31-30-172:~/devops-git-practice$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        file1.txt
        file2.txt
        file3.txt

nothing added to commit but untracked files present (use "git add" to track)
ubuntu@ip-172-31-30-172:~/devops-git-practice$ git add file1.txt
ubuntu@ip-172-31-30-172:~/devops-git-practice$ git add file2.txt
ubuntu@ip-172-31-30-172:~/devops-git-practice$ git add file3.txt
ubuntu@ip-172-31-30-172:~/devops-git-practice$ git commit -m file1.txt
[master efacb53] file1.txt
 3 files changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 file1.txt
 create mode 100644 file2.txt
 create mode 100644 file3.txt
ubuntu@ip-172-31-30-172:~/devops-git-practice$ git log --oneline
efacb53 (HEAD -> master) file1.txt
bef475d git-commands.md
454ae68  file.txt
ubuntu@ip-172-31-30-172:~/devops-git-practice$

Task 6: Understand the Git Workflow
Answer these questions in your own words (add them to a day-22-notes.md file):

1 What is the difference between git add and git commit?
ans >>>git add	Changes ko staging area me bhejna
git commit	Staged changes ko permanent history me save karna

git add prepares changes, git commit records them permanently 

2 What does the staging area do? Why doesn't Git just commit directly?
ans >> The staging area (index) is a middle layer between your working files and the Git history.
Working Directory → Staging Area → Git Repository
 It lets you control WHAT goes into the next commit

3 What information does git log show you?
git log shows the history of commits in your repository.
1. 🆔 Commit Hash 2. 👤 Author 3. 📅 Date

4 What is the .git/ folder and what happens if you delete it?
.git/ is the heart of your Git repository

It is a hidden folder that stores everything Git needs to track your project.
1. 🧠 objects/

👉 Stores all commits, files, blobs (actual data) 
2. 🌿 refs/

👉 Stores branch pointers (like master, main) 
3. 📍 HEAD

👉 Points to current branch
4. 📦 index

👉 Staging area ka data (very important!)
5. ⚙️ config

👉 Repo-specific Git settings
What happens if you delete .git/?
rm -rf .git

🚨 Result:

❌ All commit history gone
❌ Branches gone
❌ Staging area gone
❌ Remote connection gone

👉 Your folder becomes a normal directory

5 What is the difference between a working directory, staging area, and repository?

Working Directory	Where you edit files
Staging Area	Where you prepare changes
Repository	Where commits are permanently stored

working Directory 🧑‍💻

👉 Ye tumhari actual files ka area hai
Jaha tum code likhte ho / edit karte ho
Changes yahin pe hote hain
echo "hello" > file.txt

Staging Area 📥 (Index)
👉 Ye middle layer hai
Tum decide karte ho kya commit hoga
Controlled selection
Ye permanent storage (history) hai
Commit yahan save hota hai
Version control yahin maintain hota hai
git commit -m "Added file"


