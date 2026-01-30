The core components of Linux (kernel, user space, init/systemd)
Core Components of Linux
1. Kernel
The kernel is the heart of Linux. It directly interacts with hardware and manages system resources.
Key responsibilities:
Process scheduling (which process runs on CPU)
Memory management (RAM, swap)
Device drivers (disk, network, USB)
System calls (interface between user programs and hardware)
👉 Applications never talk to hardware directly — they talk to the kernel.
2. User Space
User space is where all normal programs run:
Shells (bash, zsh)
System utilities (ls, ps, top, grep)
Services (nginx, docker, kubelet)
User applications
User-space programs:
Cannot access hardware directly
Must request services via system calls to the kernel
3. init / systemd
When Linux boots, the kernel starts PID 1, which is:
systemd (on most modern Linux distributions)
systemd is responsible for:
Starting system services
Managing service dependencies
Restarting failed services
Handling system boot and shutdown

How Processes Are Created and Managed ?
Process Creation
A process calls fork() → creates a child process
Child process calls exec() → loads a new program
Kernel assigns:
PID (Process ID)
Memory space
CPU scheduling
Example:
ps -ef
Shows all running processes and their parent-child relationships.
Process Management by Kernel
The kernel manages processes by:
Scheduling CPU time (fair usage)
Tracking states (running, sleeping, zombie)
Handling signals (SIGKILL, SIGTERM)
Important commands:
ps, top, htop
kill, nice, uptime


What systemd Does and Why It Matters
What systemd Is
systemd is:
The init system
A service manager
A process supervisor
It uses units, such as:
.service → services (nginx, docker)
.target → system states (multi-user, graphical)
Why systemd Is Critical for DevOps
Automatically restarts failed services
Controls startup order (dependencies)
Centralized logging via journalctl
Used heavily in containers, Kubernetes nodes, cloud VMs
Common commands:
systemctl status nginx
systemctl restart docker
journalctl -u kubelet

systemctl status nginx
systemctl restart docker
journalctl -u kubelet
DevOps Troubleshooting Mindset
When something breaks, always ask:
Is the process running?
Did systemd fail to start it?
Is the kernel under CPU/memory pressure?
Linux is predictable — if you understand its internals.