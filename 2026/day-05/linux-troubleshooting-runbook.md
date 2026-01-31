cpu health check 
>>>cpu load kaise check kare 
>>uptime command se load average se core ko compare krna hai agar load avrage jada hai  core se to  cpu health gadbad hai >> vie versa 

ubuntu@ip-172-31-29-11:~$ uptime
 20:09:29 up  2:23,  1 user,  load average: 0.00, 0.00, 0.00
ubuntu@ip-172-31-29-11:~$ top
top - 20:09:46 up  2:23,  1 user,  load average: 0.00, 0.00, 0.00
Tasks: 109 total,   1 running, 108 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.0 us,  0.3 sy,  0.0 ni, 89.2 id,  0.3 wa,  0.0 hi,  0.0 si, 10.2 st
MiB Mem :    957.3 total,    108.8 free,    387.4 used,    626.3 buff/cache
MiB Swap:      0.0 total,      0.0 free,      0.0 used.    569.9 avail Mem

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
      1 root      20   0   22272  13708   9652 S   0.0   1.4   0:02.14 systemd
      2 root      20   0       0      0      0 S   0.0   0.0   0:00.00 kthreadd
      3 root      20   0       0      0      0 S   0.0   0.0   0:00.00 pool_workqueue_release
      4 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-rcu_gp
      5 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-sync_wq
      6 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-kvfree_rcu_+
      7 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-slub_flushwq
      8 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-netns
     10 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/0:0H-events_h+
     13 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-mm_percpu_wq
     14 root      20   0       0      0      0 I   0.0   0.0   0:00.00 rcu_tasks_rude_kthread
     15 root      20   0       0      0      0 I   0.0   0.0   0:00.00 rcu_tasks_trace_kthre+
     16 root      20   0       0      0      0 S   0.0   0.0   0:00.26 ksoftirqd/0
     17 root      20   0       0      0      0 I   0.0   0.0   0:00.32 rcu_sched
     18 root      20   0       0      0      0 S   0.0   0.0   0:00.00 rcu_exp_par_gp_kthrea+
     19 root      20   0       0      0      0 S   0.0   0.0   0:00.00 rcu_exp_gp_kthread_wo+
     20 root      rt   0       0      0      0 S   0.0   0.0   0:00.04 migration/0
     21 root     -51   0       0      0      0 S   0.0   0.0   0:00.00 idle_inject/0
     22 root      20   0       0      0      0 S   0.0   0.0   0:00.00 cpuhp/0
     23 root      20   0       0      0      0 S   0.0   0.0   0:00.00 kdevtmpfs
     24 root       0 -20       0      0      0 I   0.0   0.0   0:00.00 kworker/R-inet_frag_wq


memory  health check 

free -m vmstat
health check karne k liye check krenge total used free available and swap 


ubuntu@ip-172-31-29-11:~$ free -m
               total        used        free      shared  buff/cache   available
Mem:             957         387         108           0         626         570
Swap:              0           0           0
ubuntu@ip-172-31-29-11:~$ vmstat
procs -----------memory---------- ---swap-- -----io---- -system-- -------cpu-------
 r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st gu
 0  0      0 111200  13640 628196    0    0   124   138  108    0  1  0 85  0 14  0

Disk   health check 

df -h  and lsblk se check krenge kon se mount point pe use jada ho rha hai 

ubuntu@ip-172-31-29-11:~$ df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/root       6.8G  2.5G  4.3G  37% /
tmpfs           479M     0  479M   0% /dev/shm
tmpfs           192M  900K  191M   1% /run
tmpfs           5.0M     0  5.0M   0% /run/lock
/dev/xvda16     881M   89M  730M  11% /boot
/dev/xvda15     105M  6.2M   99M   6% /boot/efi
tmpfs            96M   12K   96M   1% /run/user/1000
ubuntu@ip-172-31-29-11:~$ lsblk
NAME     MAJ:MIN RM  SIZE RO TYPE MOUNTPOINTS
loop0      7:0    0 27.8M  1 loop /snap/amazon-ssm-agent/12322
loop1      7:1    0 27.6M  1 loop /snap/amazon-ssm-agent/11797
loop2      7:2    0   74M  1 loop /snap/core22/2292
loop3      7:3    0 48.1M  1 loop /snap/snapd/25935
loop4      7:4    0 50.9M  1 loop /snap/snapd/25577
loop5      7:5    0   74M  1 loop /snap/core22/2163
xvda     202:0    0    8G  0 disk
├─xvda1  202:1    0    7G  0 part /
├─xvda14 202:14   0    4M  0 part
├─xvda15 202:15   0  106M  0 part /boot/efi
└─xvda16 259:0    0  913M  0 part /boot

network    health check 

1.  interface up hai ya nahi ye check krenge 
enX0: <BROADCAST,MULTICAST,UP,LOWER_UP >>agar up lower up hai to okk 
warna up krenge  command se >> ip link set eth0 up

ubuntu@ip-172-31-29-11:~$ ip addr
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute
       valid_lft forever preferred_lft forever
2: enX0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 9001 qdisc fq_codel state UP group default qlen 1000
    link/ether 02:15:ec:2c:62:53 brd ff:ff:ff:ff:ff:ff
    inet 172.31.29.11/20 metric 100 brd 172.31.31.255 scope global dynamic enX0
       valid_lft 2717sec preferred_lft 2717sec
    inet6 fe80::15:ecff:fe2c:6253/64 scope link
       valid_lft forever preferred_lft forever
3: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default
    link/ether ce:13:b7:e0:44:7b brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.1/16 brd 172.17.255.255 scope global docker0
       valid_lft forever preferred_lft forever

2. ip address mila hai ya nahi check krenge 

ip rout  mai default  ip check krenge 

ubuntu@ip-172-31-29-11:~$ ip rout
default via 172.31.16.1 dev enX0 proto dhcp src 172.31.29.11 metric 100
172.17.0.0/16 dev docker0 proto kernel scope link src 172.17.0.1 linkdown
172.31.0.2 via 172.31.16.1 dev enX0 proto dhcp src 172.31.29.11 metric 100
172.31.16.0/20 dev enX0 proto kernel scope link src 172.31.29.11 metric 100
172.31.16.1 dev enX0 proto dhcp scope link src 172.31.29.11 metric 100

3. ping kar k test krenge  connectivity ko 

ping command se check krenge  ping ho rha ya  nahi 
7 packets transmitted, 7 received, 0% packet loss, time 6011ms

ubuntu@ip-172-31-29-11:~$ ping 8.8.8.8
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=117 time=7.98 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=117 time=7.55 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=117 time=7.78 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=117 time=7.82 ms
64 bytes from 8.8.8.8: icmp_seq=5 ttl=117 time=7.54 ms
64 bytes from 8.8.8.8: icmp_seq=6 ttl=117 time=7.52 ms
64 bytes from 8.8.8.8: icmp_seq=7 ttl=117 time=7.80 ms
^C
--- 8.8.8.8 ping statistics ---
7 packets transmitted, 7 received, 0% packet loss, time 6011ms
rtt min/avg/max/mdev = 7.520/7.711/7.978/0.165 ms

4. ports check krenge ss -tulnp 

if port unknown aa rha to root se check krenge 
if listn aa rha to okk warna 
Port LISTEN nahi
Ya port hi missing
Service DOWN ya start nahi hui

ubuntu@ip-172-31-29-11:~$ ss -tulnp
Netid   State    Recv-Q   Send-Q         Local Address:Port      Peer Address:Port  Process
udp     UNCONN   0        0                 127.0.0.54:53             0.0.0.0:*
udp     UNCONN   0        0              127.0.0.53%lo:53             0.0.0.0:*
udp     UNCONN   0        0          172.31.29.11%enX0:68             0.0.0.0:*
udp     UNCONN   0        0                  127.0.0.1:323            0.0.0.0:*
udp     UNCONN   0        0                      [::1]:323               [::]:*
tcp     LISTEN   0        4096               127.0.0.1:46667          0.0.0.0:*
tcp     LISTEN   0        4096           127.0.0.53%lo:53             0.0.0.0:*
tcp     LISTEN   0        4096              127.0.0.54:53             0.0.0.0:*
tcp     LISTEN   0        511                  0.0.0.0:80             0.0.0.0:*
tcp     LISTEN   0        4096                 0.0.0.0:22             0.0.0.0:*
tcp     LISTEN   0        511                     [::]:80                [::]:*
tcp     LISTEN   0        4096                    [::]:22                [::]:*

5 . dns check krenge working hai ya nahi 

nslookup google.com se check krenge 
Name:   google.com
Address: 142.251.33.78
name resolve hua ya nahi ip mai 



ubuntu@ip-172-31-29-11:~$ resolvectl status
Global
         Protocols: -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
  resolv.conf mode: stub

Link 2 (enX0)
    Current Scopes: DNS
         Protocols: +DefaultRoute -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
Current DNS Server: 172.31.0.2
       DNS Servers: 172.31.0.2
        DNS Domain: us-west-2.compute.internal

Link 3 (docker0)
    Current Scopes: none
         Protocols: -DefaultRoute -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
ubuntu@ip-172-31-29-11:~$ nslookup google.com
Server:         127.0.0.53
Address:        127.0.0.53#53

Non-authoritative answer:
Name:   google.com
Address: 142.251.33.78
Name:   google.com
Address: 2607:f8b0:400a:806::200e



question 2 Trace logs for that service

ubuntu@ip-172-31-29-11:~$ systemctl status ssh
● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/usr/lib/systemd/system/ssh.service; disabled; preset: enabled)
    Drop-In: /usr/lib/systemd/system/ssh.service.d
             └─ec2-instance-connect.conf
     Active: active (running) since Sat 2026-01-31 18:37:24 UTC; 2h 8min ago
TriggeredBy: ● ssh.socket
       Docs: man:sshd(8)
             man:sshd_config(5)
    Process: 7399 ExecStartPre=/usr/sbin/sshd -t (code=exited, status=0/SUCCESS)
   Main PID: 7422 (sshd)
      Tasks: 1 (limit: 1121)
     Memory: 3.5M (peak: 4.2M)
        CPU: 525ms
     CGroup: /system.slice/ssh.service
             └─7422 "sshd: /usr/sbin/sshd -D -o AuthorizedKeysCommand /usr/share/ec2-instance>

Jan 31 19:26:39 ip-172-31-29-11 sshd[8464]: Accepted publickey for ubuntu from 152.58.114.132>
Jan 31 19:26:39 ip-172-31-29-11 sshd[8464]: pam_unix(sshd:session): session opened for user u>
Jan 31 19:33:37 ip-172-31-29-11 sshd[8559]: Accepted publickey for ubuntu from 152.58.114.132>
Jan 31 19:33:37 ip-172-31-29-11 sshd[8559]: pam_unix(sshd:session): session opened for user u>
Jan 31 19:49:10 ip-172-31-29-11 sshd[8689]: Accepted publickey for ubuntu from 152.58.114.132>
Jan 31 19:49:10 ip-172-31-29-11 sshd[8689]: pam_unix(sshd:session): session opened for user u>
Jan 31 20:09:14 ip-172-31-29-11 sshd[8839]: Accepted publickey for ubuntu from 152.58.114.132>
Jan 31 20:09:14 ip-172-31-29-11 sshd[8839]: pam_unix(sshd:session): session opened for user u>
Jan 31 20:45:07 ip-172-31-29-11 sshd[9066]: Accepted publickey for ubuntu from 152.58.114.132>
Jan 31 20:45:07 ip-172-31-29-11 sshd[9066]: pam_unix(sshd:session): session opened for user u>

ubuntu@ip-172-31-29-11:~$ journalctl -u ssh
Jan 31 03:56:59 ip-172-31-29-11 systemd[1]: Starting ssh.service - OpenBSD Secure Shell serve>
Jan 31 03:56:59 ip-172-31-29-11 sshd[1002]: Server listening on 0.0.0.0 port 22.
Jan 31 03:56:59 ip-172-31-29-11 sshd[1002]: Server listening on :: port 22.

Jan 31 05:13:37 ip-172-31-29-11 sshd[3162]: pam_unix(sshd:session): session opened for user u>
Jan 31 06:36:08 ip-172-31-29-11 systemd[1]: Stopping ssh.service - OpenBSD Secure Shell serve>
Jan 31 06:36:08 ip-172-31-29-11 sshd[1002]: Received signal 15; terminating.
Jan 31 06:36:08 ip-172-31-29-11 systemd[1]: ssh.service: Deactivated successfully.
Jan 31 06:36:08 ip-172-31-29-11 systemd[1]: Stopped ssh.service - OpenBSD Secure Shell server.
-- Boot bfcf76943803418ea61bde6be2c38c5a --
Jan 31 17:51:41 ip-172-31-29-11 systemd[1]: Starting ssh.service - OpenBSD Secure Shell serve>
Jan 31 17:51:41 ip-172-31-29-11 sshd[1235]: Server listening on 0.0.0.0 port 22.
Jan 31 17:51:41 ip-172-31-29-11 sshd[1235]: Server listening on :: port 22.
Jan 31 17:51:41 ip-172-31-29-11 systemd[1]: Started ssh.service - OpenBSD Secure Shell server.
Jan 31 17:51:48 ip-172-31-29-11 sshd[1236]: Connection closed by authenticating user ubuntu 1>
Jan 31 17:52:25 ip-172-31-29-11 sshd[1241]: Accepted publickey for ubuntu from 152.58.114.132>
Jan 31 17:52:25 ip-172-31-29-11 sshd[1241]: pam_unix(sshd:session): session opened for user u>
Jan 31 18:00:58 ip-172-31-29-11 sshd[1380]: Connection closed by 104.248.85.226 port 35292

Jan 31 18:11:20 ip-172-31-29-11 sshd[1426]: Accepted publickey for ubuntu from 152.58.114.132>
Jan 31 18:11:20 ip-172-31-29-11 sshd[1426]: pam_unix(sshd:session): session opened for user u>
Jan 31 18:31:02 ip-172-31-29-11 sshd[1542]: Accepted publickey for ubuntu from 152.58.114.132>
Jan 31 18:31:02 ip-172-31-29-11 sshd[1542]: pam_unix(sshd:session): session opened for user u>
Jan 31 18:34:15 ip-172-31-29-11 sshd[1627]: Connection closed by 178.62.207.114 port 57948
J
Jan 31 18:37:23 ip-172-31-29-11 sshd[1235]: Received signal 15; terminating.
Jan 31 18:37:23 ip-172-31-29-11 systemd[1]: Stopping ssh.service - OpenBSD Secure Shell serve>
Jan 31 18:37:24 ip-172-31-29-11 sshd[7422]: Server listening on 0.0.0.0 port 22.
Jan 31 18:37:24 ip-172-31-29-11 sshd[7422]: Server listening on :: port 22.
Jan 31 18:37:30 ip-172-31-29-11 sshd[7564]: Connection closed by authenticating user root 178>

Jan 31 18:11:20 ip-172-31-29-11 sshd[1426]: Accepted publickey for ubuntu from 152.58.114.132>
Jan 31 18:11:20 ip-172-31-29-11 sshd[1426]: pam_unix(sshd:session): session opened for user u>
Jan 31 18:31:02 ip-172-31-29-11 sshd[1542]: Accepted publickey for ubuntu from 152.58.114.132>
Jan 31 18:31:02 ip-172-31-29-11 sshd[1542]: pam_unix(sshd:session): session opened for user u>
Jan 31 18:34:15 ip-172-31-29-11 sshd[1627]: Connection closed by 178.62.207.114 port 57948
Jan 31 18:34:16 ip-172-31-29-11 sshd[1628]: Connection closed by 178.128.254.224 port 57994
Jan 31 18:35:17 ip-172-31-29-11 sshd[1632]: Connection closed by authenticating user root 178>
Jan 31 18:35:42 ip-172-31-29-11 sshd[1634]: Connection closed by authenticating user root 178>
Jan 31 18:36:20 ip-172-31-29-11 sshd[1638]: Connection closed by authenticating user root 178>
Jan 31 18:36:38 ip-172-31-29-11 sshd[2053]: Connection closed by authenticating user root 178>
Jan 31 18:37:03 ip-172-31-29-11 sshd[2925]: Connection closed by authenticating user root 178>
Jan 31 18:37:23 ip-172-31-29-11 sshd[1235]: Received signal 15; terminating.
Jan 31 18:37:23 ip-172-31-29-11 systemd[1]: Stopping ssh.service - OpenBSD Secure Shell serve>
Jan 31 18:37:24 ip-172-31-29-11 sshd[7422]: Server listening on 0.0.0.0 port 22.
Jan 31 18:37:24 ip-172-31-29-11 sshd[7422]: Server listening on :: port 22.
Jan 31 18:37:30 ip-172-31-29-11 sshd[7564]: Connection closed by authenticating user root 178>
Jan 31 18:38:11 ip-172-31-29-11 sshd[8230]: Connection closed by authenticating user root 178>
Jan 31 18:38:23 ip-172-31-29-11 sshd[8232]: Connection closed by authenticating user root 178>
Jan 31 18:38:11 ip-172-31-29-11 sshd[8230]: Connection closed by authenticating user root 178>
Jan 31 18:38:23 ip-172-31-29-11 sshd[8232]: Connection closed by authenticating user root 178>
Jan 31 18:39:13 ip-172-31-29-11 sshd[8241]: Connection closed by authenticating user root 178>
Jan 31 18:39:15 ip-172-31-29-11 sshd[8243]: Connection closed by authenticating user root 178>
Jan 31 18:40:04 ip-172-31-29-11 sshd[8245]: Connection closed by 178.128.254.224 port 48862
Jan 31 18:40:05 ip-172-31-29-11 sshd[8246]: Connection closed by authenticating user root 178>
Jan 31 18:40:29 ip-172-31-29-11 sshd[8250]: Connection closed by 161.35.89.155 port 47934
Jan 31 18:40:46 ip-172-31-29-11 sshd[8251]: error: kex_exchange_identification: read: Connect>
Jan 31 18:40:46 ip-172-31-29-11 sshd[8251]: Connection reset by 178.128.254.224 port 42748
Jan 31 18:40:47 ip-172-31-29-11 sshd[8252]: Connection closed by authenticating user root 178>
Jan 31 18:41:54 ip-172-31-29-11 sshd[8254]: Connection closed by authenticating user root 161>
Jan 31 18:42:45 ip-172-31-29-11 sshd[8262]: Connection closed by authenticating user root 161>
Jan 31 18:43:35 ip-172-31-29-11 sshd[8264]: Connection closed by authenticating user root 161>
Jan 31 18:44:26 ip-172-31-29-11 sshd[8266]: Connection closed by authenticating user root 161>
Jan 31 18:45:17 ip-172-31-29-11 sshd[8271]: Connection closed by authenticating user root 161>
Jan 31 18:46:08 ip-172-31-29-11 sshd[8274]: Connection closed by authenticating user root 161>
Jan 31 18:46:56 ip-172-31-29-11 sshd[8276]: Connection closed by authenticating user root 161>
Jan 31 19:14:41 ip-172-31-29-11 sshd[8303]: Accepted publickey for ubuntu from 152.58.114.132>
Jan 31 19:14:41 ip-172-31-29-11 sshd[8303]: pam_unix(sshd:session): session opened for user u>
Jan 31 19:26:39 ip-172-31-29-11 sshd[8464]: Accepted publickey for ubuntu from 152.58.114.132>
Jan 31 19:26:39 ip-172-31-29-11 sshd[8464]: pam_unix(sshd:session): session opened for user u>
Jan 31 19:33:37 ip-172-31-29-11 sshd[8559]: Accepted publickey for ubuntu from 152.58.114.132>
Jan 31 19:33:37 ip-172-31-29-11 sshd[8559]: pam_unix(sshd:session): session opened for user u>
Jan 31 19:49:10 ip-172-31-29-11 sshd[8689]: Accepted publickey for ubuntu from 152.58.114.132>
Jan 31 19:49:10 ip-172-31-29-11 sshd[8689]: pam_unix(sshd:session): session opened for user u>
Jan 31 20:09:14 ip-172-31-29-11 sshd[8839]: Accepted publickey for ubuntu from 152.58.114.132>
Jan 31 20:09:14 ip-172-31-29-11 sshd[8839]: pam_unix(sshd:session): session opened for user u>
lines 61-87/89 97%


3. Write a mini runbook describing what you did and what you’d do next if things were worse
🎯 Objective

2–3 minutes me server ki overall health verify karna (CPU, Memory, Disk, Network) and decide next action.

🧪 What I Did (Initial Health Check)
1️⃣ CPU Health

Commands

uptime
top


Checked

Load average vs CPU cores

CPU idle (%id)

I/O wait (%wa)

Top CPU-consuming processes

Result

Load < cores

Idle > 60%

No abnormal wait

✅ CPU healthy

2️⃣ Memory Health

Commands

free -h
vmstat 1 5


Checked

Available memory (not free)

Swap usage

si/so (swap in/out)

Result

Available memory sufficient

Swap not actively used

No memory pressure

✅ Memory healthy

3️⃣ Disk Health

Commands

df -h
lsblk
du -sh /var/*


Checked

Disk usage %

Critical mounts (/, /var)

Largest space-consuming directories

Partition layout

Result

No critical mount > 80%

Disk structure normal

No immediate risk

✅ Disk healthy

4️⃣ Network & DNS Health

Commands

ip addr
ip route
ping 8.8.8.8
nslookup google.com
resolvectl status


Checked

Interface UP + IP assigned

Default route present

Internet reachability

DNS resolution

Upstream DNS server

Result

Interface enX0 UP

Upstream DNS = 172.31.0.2 (AWS VPC DNS)

DNS resolution successful

✅ Network & DNS healthy

🟢 Overall Verdict

Server is HEALTHY
No CPU, memory, disk, or network bottlenecks detected.

🔴 What I’d Do Next If Things Were Worse (Escalation Plan)
🚨 If CPU was high

Identify top process (top, ps)

Check app logs

Restart service or scale CPU/replicas

🚨 If Memory was low / swap active

Identify memory hog process

Restart leaking service

Add RAM / tune app / caching

🚨 If Disk was >80% / full

Identify large directories (du)

Cleanup logs / docker data

Enable logrotate

Extend disk if needed

🚨 If Network / DNS failed

If IP ping fails → network issue

If DNS fails → check systemd-resolved

Restart DNS service

Test with alternate DNS (8.8.8.8)

Check firewall / security groups