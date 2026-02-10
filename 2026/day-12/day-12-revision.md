Mindset & plan: revisit your Day 01 learning plan—are your goals still right? any tweaks?

done 


Processes & services: rerun 2 commands from Day 04/05 (e.g., ps, systemctl status, journalctl -u <service>); jot what you observed today.

ps
ps -ef
ps aux

top
htop

top
ps aux --sort=-%cpu
ps aux --sort=-%mem

sleep 100
sleep 100 &  ,jobs >>background job dekhne k liye 

Signals & kill (MOST IMPORTANT 🔥)
Common signals
Signal	Number	Meaning
SIGTERM	15	Graceful stop
SIGKILL	9	Force kill
SIGSTOP	19	Pause
SIGCONT	18	Resume
kill  
kill PID
kill -9 PID

nice & renice (Priority control)
nice -n 10 command
renice -n -5 PID 
Lower number = higher priority


🔥 Production down, SSH mil gaya, ab kya?

🥇 Top 5 Commands I’d Reach For First
1️⃣ ls -l

Permission

Owner

Group

Executable ya nahi

ls -l

2️⃣ ps aux / ps -ef

App chal rahi hai ya nahi?

ps aux | grep nginx

3️⃣ top

Server slow? CPU / RAM kaun kha raha?

top


(keys: P CPU, M Memory)

4️⃣ df -h

Disk full = MOST COMMON INCIDENT ❗

df -h

5️⃣ tail -f

App bol kya rahi hai (logs)

tail -f /var/log/app.log

Incident Mindset (VERY IMPORTANT)

Order 

ls -l   → ownership/permission
ps/top  → process/resource
df -h   → disk
tail    → logs


User/group sanity: recreate one small scenario from Day 09 or Day 11 (create a user or change ownership) and verify with id/ls -l 

done 

Which 3 commands save you the most time right now — and why
1. systemctl
systemctl status nginx
systemctl restart nginx


Why:
90% prod issues = service not running, failed, or misconfigured.
This command tells me status + logs hint + exit code instantly.

2. journalctl
journalctl -u nginx -n 50 --no-pager


Why:
Logs = truth.
This saves me from guessing why something failed after restart.

3. ss (or netstat)
ss -tulnp


Why:
Confirms port binding.
Service running ≠ service listening. This catches that gap fast.

2️ How do you check if a service is healthy?
Exact first 2–3 commands (order matters)
Step 1 – Service status
systemctl status myapp


✔ Running?
✖ Failed? → reason often visible here

Step 2 – Logs
journalctl -u myapp -n 50 --no-pager


✔ Errors
✔ Permission issues
✔ Missing config / env vars

Step 3 – Port / Process check
ss -tulnp | grep myapp
# OR
ps aux | grep myapp


✔ Confirms app is actually alive and reachable

💡 DevOps rule:
Green service + no port = fake healthy

3️ How do you safely change ownership & permissions (without breaking access)
Golden rule

👉 Ownership first, permissions second
👉 Never blindly use 777

Example (safe & real-world)
sudo chown -R appuser:appgroup /opt/myapp
sudo chmod 750 /opt/myapp


Why this works

appuser → full access

appgroup → read/execute

others → no access

📌 Before doing this, ALWAYS check

ls -ld /opt/myapp

4️ What will you focus on improving in the next 3 days
Day 1

Faster service failure diagnosis

systemctl → journalctl → ss (no hesitation)

Day 2

Permission confidence

chmod numeric vs symbolic

Understand why access breaks

Day 3

Structured troubleshooting

Don’t jump steps

Build muscle memory for the flow

⏱ Suggested Flow (30–45 minutes) — refined
10 min

Skim notes

Update Day 01 troubleshooting flow

15–20 min (hands-on)

Stop a service → fix it

Change ownership → verify access

Check logs → confirm root cause

5–10 min (write)

Answer:

What broke?

What command revealed it?

What will I try first next time?


