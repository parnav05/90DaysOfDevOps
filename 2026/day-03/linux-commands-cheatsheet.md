1. Logs & Debugging (MOST USED)
tail -f logfile              # live logs
tail -n 100 logfile          # last 100 lines
grep ERROR logfile           # find errors
grep -i warn logfile         # warnings (case-insensitive)
journalctl -u service        # service logs
journalctl -xe               # system errors
less logfile                 # safe log reading

2. Services (systemd)
systemctl status service
systemctl restart service
systemctl start service
systemctl stop service
systemctl enable service
systemctl disable service
3. Process & Resource Checks
uptime	>>Server slow / alert aaya	>>Load average dekhne ke liye	>>uptime
top	>>CPU/RAM spike check	>>Real-time process monitoring	>>top
htop	>>Easy & interactive view	Color, tree view, mouse support	htop
ps aux	>>Snapshot / scripting	>>Stable process list>>	ps aux
free -h	>>Memory issue / OOM	>>RAM & swap usage	>>free -h
kill PID	>>Single process stop	>>Graceful termination	>>kill 1234
kill -9 PId	 >>Process stuck	>>Force kill	>>kill -9 1234
pkill name	>>Multiple processes	>>Name se kill	>>pkill nginx
watch cmd	>>Continuous monitoring	>>Auto refresh output	>>watch free -h
4. Disk & File System (VERY COMMON INCIDENT)
df -h	>>Disk full alert	>>Filesystem usage dekhne	>>df -h
du -sh * >>Disk space kaun kha raha	>>Directory-wise size	>>du -sh *
ls -lah	>>Files detail chahiye	>>Permissions, size, hidden files	>>ls -lah
cd	D>>irectory change	>>Location move karna	>>cd /var/log
pwd	>>Current path	>>Exact location jaanne	>>pwd
rm -rf file >>File/dir delete	>>Force remove	>>rm -rf test/ ⚠️
cp file1 file2	>>File copy	>>Backup / duplicate	>>cp a.txt b.txt
mv old new	>>>Rename / move	>>File move ya rename	>>mv old.txt new.txt
chmod	>>Permission change	>>Access control	>>chmod 755 script.sh
chown	>>Owner change	>>User/group assign	>>chown user:group file
5. Networking & Connectivity
ip addr >> Network issue / no IP >> Interface & IP check >> ip addr
ip route >> Internet nahi chal raha >> Default gateway check >> ip route
ping host >> Connectivity test >> Host reachable hai ya nahi >> ping google.com
curl url >> Website / API test >> HTTP response & content >> curl https://example.com
curl -I url >> Header check >> HTTP status only >> curl -I https://example.com
ss -tulnp >> Port issue >> Listening ports + PID >> ss -tulnp
dig domain >> DNS deep debug >> DNS records detail >> dig google.com
nslookup domain >> Basic DNS check >> Name → IP resolution >> nslookup google.com
