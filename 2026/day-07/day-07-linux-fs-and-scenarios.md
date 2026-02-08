/ (root)

This is the starting point of the Linux file system.

All files and directories exist under /.
Command:
ls -l /
You will see:
bin, etc, home, var, usr

/home
This directory contains home folders for normal users.
User files, scripts, SSH keys, and personal data live here.
mmand:
ls -l /home
You will see:
User directories like user1, parnav
I would use this when:
I need to debug user issues or check user-owned scripts and files.

/root
This is the home directory of the root (admin) user.
Normal users cannot access it.
Command:
ls -l /root
You will see:
Admin scripts and configuration files
I would use this when:
I need to perform emergency or admin-level troubleshooting.

/etc
This directory contains system and application configuration files.
Most service configuration files are stored here.
Command:
ls -l /etc
You will see:
hostname, hosts, ssh, systemd
I would use this when:
I need to change or debug service configurations.

/var/log
This directory stores system and application log files.
Logs are very important for troubleshooting.
Command:
ls -l /var/log
You will see:
syslog, auth.log, journal
I would use this when:
A service fails, crashes, or shows errors.

/tmp
This directory is used for temporary files.
Files here are usually removed after reboot.
Command:
ls -l /tmp
You will see:
Temporary files and folders
I would use this when:
I need a place for temporary testing or downloads.




senario 1 :
A web application service called 'myapp' failed to start after a server reboot.
What commands would you run to diagnose the issue?
Write at least 4 commands in order.

systemctl status ssh
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/usr/lib/systemd/system/ssh.service; disabled; preset: enabl>
    Drop-In: /usr/lib/systemd/system/ssh.service.d
             └─ec2-instance-connect.conf
     Active: active (running) since Sun 2026-02-08 17:28:19 UTC; 1min 46s ago
TriggeredBy: ● ssh.socket
       Docs: man:sshd(8)
             man:sshd_config(5)
    Process: 1030 ExecStartPre=/usr/sbin/sshd -t (code=exited, status=0/SUCCESS)
   Main PID: 1032 (sshd)
      Tasks: 1 (limit: 1008)
     Memory: 4.8M (peak: 5.4M)
        CPU: 52ms
     CGroup: /system.slice/ssh.service
             └─1032 "sshd: /usr/sbin/sshd -D -o AuthorizedKeysCommand /usr/share/>

systemctl is-enabled ssh
disabled


ubuntu@ip-172-31-38-49:~$ journalctl -u cronyd
-- No entries --

senario 2 
Your manager reports that the application server is slow.
You SSH into the server. What commands would you run to identify
which process is using high CPU?

>>top or htop command for live cpu usage 
top - 17:36:27 up 8 min,  1 user,  load average: 0.00, 0.00, 0.00
Tasks: 109 total,   1 running, 108 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.0 us,  0.0 sy,  0.0 ni,100.0 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
MiB Mem :    914.2 total,    357.5 free,    340.0 used,    374.6 buff/cache
MiB Swap:      0.0 total,      0.0 free,      0.0 used.    574.2 avail Mem

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
      1 root      20   0   22636  13832   9648 S   0.0   1.5   0:01.85 systemd
      2 root      20   0       0      0      0 S   0.0   0.0   0:00.00 kthreadd
      3 root      20   0       0      0      0 S   0.0   0.0   0:00.00 pool_work+
      4 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R+
      5 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R+
      6 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R+
      7 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R+
      8 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R+
      9 root      20   0       0      0      0 I   0.0   0.0   0:00.00 kworker/0+
     10 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/0+
     11 root      20   0       0      0      0 I   0.0   0.0   0:00.03 kworker/0+
     12 root      20   0       0      0      0 I   0.0   0.0   0:00.13 kworker/u+
     13 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R+
     14 root      20   0       0      0      0 I   0.0   0.0   0:00.00 rcu_tasks+
     15 root      20   0       0      0      0 I   0.0   0.0   0:00.00 rcu_tasks+
     16 root      20   0       0      0      0 S   0.0   0.0   0:00.02 ksoftirqd+
     17 root      20   0       0      0      0 I   0.0   0.0   0:00.06 rcu_sched

ubuntu@ip-172-31-38-49:~$ ps -aux --sort=-%cpu| head -10
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.2  1.4  22636 13832 ?        Ss   17:27   0:01 /sbin/init
root         613  0.1  4.0 1923120 38096 ?       Ssl  17:27   0:00 /usr/lib/snapd/snapd
root         966  0.0  2.1 1830624 20260 ?       Ssl  17:27   0:00 /snap/amazon-ssm-agent/11797/amazon-ssm-agent
ubuntu      1143  0.0  0.7  14992  7136 ?        S    17:28   0:00 sshd: ubuntu@pts/0
root         128  0.0  1.5  50428 14064 ?        S<s  17:27   0:00 /usr/lib/systemd/systemd-journald
root         199  0.0  0.8  26484  8328 ?        Ss   17:27   0:00 /usr/lib/systemd/systemd-udevd
systemd+     332  0.0  1.3  21592 13036 ?        Ss   17:27   0:00 /usr/lib/systemd/systemd-resolved
root          12  0.0  0.0      0     0 ?        I    17:27   0:00 [kworker/u8:0-events_unbound]
root         606  0.0  2.2  32416 20744 ?        Ss   17:27   0:00 /usr/bin/python3 /usr/bin/networkd-dispatcher --run-startup-triggers
ubuntu@ip-172-31-38-49:~$
senario 4 : 
A script at /home/user/backup.sh is not executing.
When you run it: ./backup.sh
You get: "Permission denied"

What commands would you use to fix this?

ubuntu@ip-172-31-38-49:~$ vi backup.sh
ubuntu@ip-172-31-38-49:~$ ./backup.sh
-bash: ./backup.sh: Permission denied
ubuntu@ip-172-31-38-49:~$ ls -lh backup.sh
-rw-rw-r-- 1 ubuntu ubuntu 50 Feb  8 17:56 backup.sh
ubuntu@ip-172-31-38-49:~$ chmod 764 backup.sh
ubuntu@ip-172-31-38-49:~$ vi backup.sh
ubuntu@ip-172-31-38-49:~$ ./backup.sh
hay this taking backup of the file
./backup.sh: line 4: :wq: command not found
ubuntu@ip-172-31-38-49:~$ vi backup.sh
ubuntu@ip-172-31-38-49:~$ ./backup.sh
hay this taking backup of the file
ubuntu@ip-172-31-38-49:~$
