root@DESKTOP-2PGT0AC:/home# cd parnav/
root@DESKTOP-2PGT0AC:/home/parnav# ls
app.log  company_data.txt  echo  nano
root@DESKTOP-2PGT0AC:/home/parnav# touch notes.txt
root@DESKTOP-2PGT0AC:/home/parnav# ls
app.log  company_data.txt  echo  nano  notes.txt
root@DESKTOP-2PGT0AC:/home/parnav# vim notes.txt
root@DESKTOP-2PGT0AC:/home/parnav# echo "this is a challange i have to compleate in as soon as possible " > notes.txt
root@DESKTOP-2PGT0AC:/home/parnav# cat notes.txt
this is a challange i have to compleate in as soon as possible
root@DESKTOP-2PGT0AC:/home/parnav# echo "line 1 " >> notes.txt
root@DESKTOP-2PGT0AC:/home/parnav# cat notes.txt
this is a challange i have to compleate in as soon as possible
line 1
root@DESKTOP-2PGT0AC:/home/parnav# man tee
root@DESKTOP-2PGT0AC:/home/parnav# echo "line 3" notes.txt
line 3 notes.txt
root@DESKTOP-2PGT0AC:/home/parnav# cat notes.txt
this is a challange i have to compleate in as soon as possible
line 1
root@DESKTOP-2PGT0AC:/home/parnav# ls
app.log  company_data.txt  echo  nano  notes.txt
root@DESKTOP-2PGT0AC:/home/parnav# ls -lh
total 20K
-rw-r--r-- 1 parnav parnav 1.4K Jan 15 05:28 app.log
-rw-r--r-- 1 parnav parnav  929 Jan 15 04:30 company_data.txt
-rw-r--r-- 1 parnav parnav 1.5K Jan 30 10:45 echo
-rw-r--r-- 1 parnav parnav 1.5K Jan 30 10:45 nano
-rw-r--r-- 1 root   root     72 Feb  2 03:50 notes.txt
root@DESKTOP-2PGT0AC:/home/parnav# rm echo
root@DESKTOP-2PGT0AC:/home/parnav# rm nano
root@DESKTOP-2PGT0AC:/home/parnav# ls
app.log  company_data.txt  notes.txt
root@DESKTOP-2PGT0AC:/home/parnav# cat notes.txt
this is a challange i have to compleate in as soon as possible
line 1
root@DESKTOP-2PGT0AC:/home/parnav# echo "line 3" |tee -a notes.txt
line 3
root@DESKTOP-2PGT0AC:/home/parnav# cat notes.txt
this is a challange i have to compleate in as soon as possible
line 1
line 3
root@DESKTOP-2PGT0AC:/home/parnav# head -n 2 notes.txt
this is a challange i have to compleate in as soon as possible
line 1
root@DESKTOP-2PGT0AC:/home/parnav# head -3 notes.txt
this is a challange i have to compleate in as soon as possible
line 1
line 3
root@DESKTOP-2PGT0AC:/home/parnav# ls
app.log  company_data.txt  notes.txt
root@DESKTOP-2PGT0AC:/home/parnav# ls | tee -a notes.txt
app.log
company_data.txt
notes.txt
root@DESKTOP-2PGT0AC:/home/parnav# cat notes.txt
this is a challange i have to compleate in as soon as possible
line 1
line 3
app.log
company_data.txt
notes.txt
root@DESKTOP-2PGT0AC:/home/parnav#




