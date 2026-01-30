parnav@DESKTOP-2PGT0AC:~$ top
top - 10:39:07 up  6:30,  1 user,  load average: 0.00, 0.00, 0.00
Tasks:  24 total,   1 running,  23 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.0 us,  0.1 sy,  0.0 ni, 99.9 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
MiB Mem :   5840.2 total,   5274.7 free,    504.0 used,    209.1 buff/cache
MiB Swap:   2048.0 total,   2048.0 free,      0.0 used.   5336.2 avail Mem

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
      1 root      20   0   21712  12248   9048 S   0.0   0.2   0:01.63 systemd
      2 root      20   0    3120   1920   1920 S   0.0   0.0   0:00.01 init-systemd(Ub
      6 root      20   0    3136   1792   1792 S   0.0   0.0   0:00.00 init
     55 root      19  -1   66832  19132  18236 S   0.0   0.3   0:00.96 systemd-journal
    102 root      20   0   25268   6272   4864 S   0.0   0.1   0:00.36 systemd-udevd
    154 systemd+  20   0   21452  12672  10496 S   0.0   0.2   0:00.26 systemd-resolve
    165 systemd+  20   0   91020   7680   6784 S   0.0   0.1   0:00.29 systemd-timesyn
    174 root      20   0    4236   2560   2304 S   0.0   0.0   0:00.04 cron
    175 message+  20   0    9660   4992   4480 S   0.0   0.1   0:00.32 dbus-daemon
    188 root      20   0   17964   8448   7552 S   0.0   0.1   0:00.20 systemd-logind
    190 root      20   0 1978444  15488  10624 S   0.0   0.3   0:00.64 wsl-pro-service
    206 syslog    20   0  222508   5504   4352 S   0.0   0.1   0:00.26 rsyslogd
    211 root      20   0    3160   1920   1792 S   0.0   0.0   0:00.00 agetty
    214 root      20   0    3116   1792   1664 S   0.0   0.0   0:00.01 agetty
    231 root      20   0  107020  22272  12928 S   0.0   0.4   0:00.12 unattended-upgr
    298 root      20   0    6692   3968   3456 S   0.0   0.1   0:00.01 login
    357 parnav    20   0   20100  10752   9088 S   0.0   0.2   0:00.14 systemd
    358 parnav    20   0   21148   3520   1792 S   0.0   0.1   0:00.00 (sd-pam)
    384 parnav    20   0    6072   4992   3456 S   0.0   0.1   0:00.01 bash
    814 polkitd   20   0  308164   7680   6912 S   0.0   0.1   0:00.04 polkitd
   1517 root      20   0    3124    904    768 S   0.0   0.0   0:00.00 SessionLeader
   1518 root      20   0    3140   1292   1152 S   0.0   0.0   0:00.01 Relay(1521)
   1521 parnav    20   0    6072   5248   3584 S   0.0   0.1   0:00.06 bash
   1645 parnav    20   0    9292   5504   3328 R   0.0   0.1   0:00.04 top

parnav@DESKTOP-2PGT0AC:~$ pgrep 357
parnav@DESKTOP-2PGT0AC:~$ pgrep 214
parnav@DESKTOP-2PGT0AC:~$ pid 214
Command 'pid' not found, but there are 20 similar ones.
parnav@DESKTOP-2PGT0AC:~$ ps 214
    PID TTY      STAT   TIME COMMAND
    214 tty1     Ss+    0:00 /sbin/agetty -o -p -- \u --noclear - linux

2. parnav@DESKTOP-2PGT0AC:~$ systemctl status ssh
Unit ssh.service could not be found.
parnav@DESKTOP-2PGT0AC:~$ systemctl status cron
● cron.service - Regular background program processing daemon
     Loaded: loaded (/usr/lib/systemd/system/cron.service; enabled; preset: enabled)
     Active: active (running) since Fri 2026-01-30 04:09:57 UTC; 6h ago
       Docs: man:cron(8)
   Main PID: 174 (cron)
      Tasks: 1 (limit: 6996)
     Memory: 680.0K (peak: 3.2M)
        CPU: 191ms
     CGroup: /system.slice/cron.service
             └─174 /usr/sbin/cron -f -P

Jan 30 07:17:01 DESKTOP-2PGT0AC CRON[1578]: pam_unix(cron:session): session closed for user root
Jan 30 08:17:01 DESKTOP-2PGT0AC CRON[1597]: pam_unix(cron:session): session opened for user root(uid=0) by root(uid=0)
Jan 30 08:17:01 DESKTOP-2PGT0AC CRON[1598]: (root) CMD (cd / && run-parts --report /etc/cron.hourly)
Jan 30 08:17:01 DESKTOP-2PGT0AC CRON[1597]: pam_unix(cron:session): session closed for user root
Jan 30 09:17:01 DESKTOP-2PGT0AC CRON[1620]: pam_unix(cron:session): session opened for user root(uid=0) by root(uid=0)
Jan 30 09:17:01 DESKTOP-2PGT0AC CRON[1621]: (root) CMD (cd / && run-parts --report /etc/cron.hourly)
Jan 30 09:17:01 DESKTOP-2PGT0AC CRON[1620]: pam_unix(cron:session): session closed for user root
Jan 30 10:17:01 DESKTOP-2PGT0AC CRON[1635]: pam_unix(cron:session): session opened for user root(uid=0) by root(uid=0)
Jan 30 10:17:01 DESKTOP-2PGT0AC CRON[1636]: (root) CMD (cd / && run-parts --report /etc/cron.hourly)
Jan 30 10:17:01 DESKTOP-2PGT0AC CRON[1635]: pam_unix(cron:session): session closed for user root


3. parnav@DESKTOP-2PGT0AC:~$ journalctl -u cron
Jan 14 08:12:34 DESKTOP-2PGT0AC systemd[1]: Started cron.service - Regular background program processing daemon.
Jan 14 08:12:34 DESKTOP-2PGT0AC (cron)[174]: cron.service: Referenced but unset environment variable evaluates to an empty string: EXTRA_OPTS
Jan 14 08:12:34 DESKTOP-2PGT0AC cron[174]: (CRON) INFO (pidfile fd = 3)
Jan 14 08:12:34 DESKTOP-2PGT0AC cron[174]: (CRON) INFO (Running @reboot jobs)
Jan 14 08:13:08 DESKTOP-2PGT0AC systemd[1]: Stopping cron.service - Regular background program processing daemon...
Jan 14 08:13:08 DESKTOP-2PGT0AC systemd[1]: cron.service: Deactivated successfully.
Jan 14 08:13:08 DESKTOP-2PGT0AC systemd[1]: Stopped cron.service - Regular background program processing daemon.
Jan 14 08:13:09 DESKTOP-2PGT0AC systemd[1]: Started cron.service - Regular background program processing daemon.
Jan 14 08:13:09 DESKTOP-2PGT0AC (cron)[165]: cron.service: Referenced but unset environment variable evaluates to an empty string: EXTRA_OPTS
Jan 14 08:13:09 DESKTOP-2PGT0AC cron[165]: (CRON) INFO (pidfile fd = 3)
Jan 14 08:13:09 DESKTOP-2PGT0AC cron[165]: (CRON) INFO (Running @reboot jobs)
Jan 14 08:13:39 DESKTOP-2PGT0AC systemd[1]: Stopping cron.service - Regular background program processing daemon...
Jan 14 08:13:39 DESKTOP-2PGT0AC systemd[1]: cron.service: Deactivated successfully.
Jan 14 08:13:39 DESKTOP-2PGT0AC systemd[1]: Stopped cron.service - Regular background program processing daemon.
Jan 14 08:13:43 DESKTOP-2PGT0AC systemd[1]: Started cron.service - Regular background program processing daemon.
Jan 14 08:13:43 DESKTOP-2PGT0AC (cron)[165]: cron.service: Referenced but unset environment variable evaluates to an empty string: EXTRA_OPTS
Jan 14 08:13:43 DESKTOP-2PGT0AC cron[165]: (CRON) INFO (pidfile fd = 3)
Jan 14 08:13:43 DESKTOP-2PGT0AC cron[165]: (CRON) INFO (Running @reboot jobs)
Jan 14 08:14:28 DESKTOP-2PGT0AC systemd[1]: Stopping cron.service - Regular background program processing daemon...
Jan 14 08:14:28 DESKTOP-2PGT0AC systemd[1]: cron.service: Deactivated successfully.
Jan 14 08:14:28 DESKTOP-2PGT0AC systemd[1]: Stopped cron.service - Regular background program processing daemon.
-- Boot a17a26be8a014416bfc9aa7109e14d56 --
Jan 14 08:17:58 DESKTOP-2PGT0AC systemd[1]: Started cron.service - Regular background program processing daemon.
Jan 14 08:17:58 DESKTOP-2PGT0AC (cron)[168]: cron.service: Referenced but unset environment variable evaluates to an empty string: EXTRA_OPTS
Jan 14 08:17:58 DESKTOP-2PGT0AC cron[168]: (CRON) INFO (pidfile fd = 3)
Jan 14 08:17:58 DESKTOP-2PGT0AC cron[168]: (CRON) INFO (Running @reboot jobs)
Jan 14 08:18:34 DESKTOP-2PGT0AC systemd[1]: Stopping cron.service - Regular background program processing daemon...
Jan 14 08:18:34 DESKTOP-2PGT0AC systemd[1]: cron.service: Deactivated successfully.
Jan 14 08:18:34 DESKTOP-2PGT0AC systemd[1]: Stopped cron.service - Regular background program processing daemon.
-- Boot 552f597393c843538aad1884e988cd69 --
Jan 14 08:22:39 DESKTOP-2PGT0AC systemd[1]: Started cron.service - Regular background program processing daemon.
Jan 14 08:22:39 DESKTOP-2PGT0AC (cron)[165]: cron.service: Referenced but unset environment variable evaluates to an empty string: EXTRA_OPTS
Jan 14 08:22:39 DESKTOP-2PGT0AC cron[165]: (CRON) INFO (pidfile fd = 3)
Jan 14 08:22:39 DESKTOP-2PGT0AC cron[165]: (CRON) INFO (Running @reboot jobs)
Jan 14 09:17:01 DESKTOP-2PGT0AC CRON[510]: pam_unix(cron:session): session opened for user root(uid=0) by root(uid=0)
Jan 14 09:17:01 DESKTOP-2PGT0AC CRON[511]: (root) CMD (cd / && run-parts --report /etc/cron.hourly)
Jan 14 09:17:01 DESKTOP-2PGT0AC CRON[510]: pam_unix(cron:session): session closed for user root
Jan 14 09:37:09 DESKTOP-2PGT0AC systemd[1]: Stopping cron.service - Regular background program processing daemon...

## 🔹 Mini Troubleshooting Flow

Problem:
Cron jobs not executing

Steps Taken:
1. Verified cron process using `pgrep`
2. Checked service status using `systemctl status`
3. Reviewed logs using `journalctl`
4. Checked system resources using `top`

Findings:
- Service running
- No errors in logs
- System under no load

Conclusion:
Issue is not with the cron service or system.
Likely problem is incorrect cron job configuration.
