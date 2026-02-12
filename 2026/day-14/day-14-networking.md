OSI layers (L1–L7) vs TCP/IP stack (Link, Internet, Transport, Application)

OSI Model & TCP/IP Model – Combined Notes (Clean Version)
1️⃣ OSI Model (7 Layers)
OSI = Open Systems Interconnection
It explains how data travels from one device to another step-by-step.
Mnemonic (bottom → top):
P D N T S P A → Please Do Not Throw Sausage Pizza Away 🍕
Layer 7 – Application
Interface between user and network
What user actually uses
Examples:
Web browser
WhatsApp
Email
Protocols:
HTTP / HTTPS
FTP
SMTP
Layer 6 – Presentation
Encryption & Decryption
Formatting & compression
Makes data readable for application
Example:
HTTPS encryption
SSL / TLS
Layer 5 – Session
Establish, maintain, terminate sessions
Controls login/session time
Example:
WhatsApp call session
Website login session
Layer 4 – Transport
Responsible for end-to-end delivery
Breaks data into segments
Error control & reliabilit
Protocols:
TCP – reliable, slow (websites, email
UDP – fast, unreliable (video call, gaming)
Layer 3 – Network
Routing
Finds best path from source to destination
Uses IP address
Device:
Router
Layer 2 – Data Link
Delivery inside same network
Uses MAC address
Error detection (CRC)
Device:
Switch
Layer 1 – Physical
Actual transmission of bits (0s & 1s)
Cables, signals, voltage
Examples:
Ethernet cable
Fiber
Wi-Fi signals
2️⃣ TCP/IP Model (4 Layers)
TCP/IP is practical implementation used in real internet.

TCP/IP Layers Mapping with OSI
OSI Model	TCP/IP Model
Application (7)	Application
Presentation (6)	Application
Session (5)	Application
Transport (4)	Transport
Network (3)	Internet
Data Link (2)	Network Access
Physical (1)	Network Access
3️⃣ TCP/IP Layers Explained
1. Application Layer
(OSI: Layer 7,6,5)
User interaction
Data formatting, encryption, session handling
Examples:
WhatsApp
Browser
Protocols:
HTTP / HTTPS
FTP
SMTP
DNS
2. Transport Layer
(OSI: Layer 4)
End-to-end communication
Port numbers
Protocols:
TCP → Reliable
UDP → Fast
3. Internet Layer
(OSI: Layer 3)
Logical addressing
Routin
Protocol:
IP (IPv4 / IPv6)
4. Network Access Layer
(OSI: Layer 2 & 1
MAC address
Physical transmission
Examples:
Ethernet
Wi-Fi
Cables
4️⃣ Protocols Summary (Simple)
Layer	Protocol
Application	HTTP, HTTPS, FTP, SMTP
Transport	TCP, UDP
Internet	IP
Network Access	MAC, Ethernet



Where IP, TCP/UDP, HTTP/HTTPS, DNS Sit in the Stack


Protocol Placement Table (Final Truth)
Protocol	OSI Layer	TCP/IP Layer	What it actually does
HTTP	Layer 7 – Application	Application	Web data transfer
HTTPS	Layer 7	Application	HTTP + Encryption
DNS	Layer 7	Application	Name → IP resolution
TCP	Layer 4 – Transport	Transport	Reliable delivery
UDP	Layer 4	Transport	Fast delivery
IP	Layer 3 – Network	Internet	Logical addressing & routing

Hands-on Checklist (run these; add 1–2 line observations)
Identity: hostname -I (or ip addr show) — note your IP.

ubuntu@ip-172-31-16-85:~$ hostname -i
172.31.16.85

Reachability: ping <target> — mention latency and packet loss.

ubuntu@ip-172-31-16-85:~$ ping -c 5 8.8.8.8
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=117 time=7.92 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=117 time=7.91 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=117 time=7.94 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=117 time=7.93 ms
64 bytes from 8.8.8.8: icmp_seq=5 ttl=117 time=7.95 ms

--- 8.8.8.8 ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4005ms
rtt min/avg/max/mdev = 7.912/7.929/7.952/0.015 ms

Path: traceroute <target> (or tracepath) — note any long hops/timeouts.
ubuntu@ip-172-31-16-85:~$ traceroute 8.8.8.8
traceroute to 8.8.8.8 (8.8.8.8), 30 hops max, 60 byte packets
 1  240.1.228.12 (240.1.228.12)  8.657 ms 240.1.228.14 (240.1.228.14)  8.616 ms 240.1.228.12 (240.1.228.12)  8.628 ms
 2  242.4.195.65 (242.4.195.65)  6.717 ms 242.4.194.195 (242.4.194.195)  8.548 ms 242.4.195.69 (242.4.195.69)  8.556 ms
 3  99.82.10.6 (99.82.10.6)  6.256 ms * *
 4  99.83.117.221 (99.83.117.221)  8.497 ms 99.82.10.9 (99.82.10.9)  8.461 ms 99.83.117.223 (99.83.117.223)  8.470 ms
 5  192.178.105.141 (192.178.105.141)  8.433 ms * *
 6  dns.google (8.8.8.8)  5.743 ms  7.466 ms  7.315 ms

Ports: ss -tulpn (or netstat -tulpn) — list one listening service and its port.
ubuntu@ip-172-31-16-85:~$ ss -tulpn
Netid   State    Recv-Q   Send-Q         Local Address:Port     Peer Address:Port   Process
udp     UNCONN   0        0                  127.0.0.1:323           0.0.0.0:*
udp     UNCONN   0        0                 127.0.0.54:53            0.0.0.0:*
udp     UNCONN   0        0              127.0.0.53%lo:53            0.0.0.0:*
udp     UNCONN   0        0          172.31.16.85%ens5:68            0.0.0.0:*
udp     UNCONN   0        0                      [::1]:323              [::]:*
tcp     LISTEN   0        4096              127.0.0.54:53            0.0.0.0:*
tcp     LISTEN   0        4096                 0.0.0.0:22            0.0.0.0:*
tcp     LISTEN   0        4096           127.0.0.53%lo:53            0.0.0.0:*
tcp     LISTEN   0        4096                    [::]:22               [::]:*

Name resolution: dig <domain> or nslookup <domain> — record the resolved IP.
ubuntu@ip-172-31-16-85:~$ dig google.com

; <<>> DiG 9.18.39-0ubuntu0.24.04.2-Ubuntu <<>> google.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 39242
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 65494
;; QUESTION SECTION:
;google.com.                    IN      A

;; ANSWER SECTION:
google.com.             146     IN      A       142.250.73.142

;; Query time: 2 msec
;; SERVER: 127.0.0.53#53(127.0.0.53) (UDP)
;; WHEN: Thu Feb 12 05:20:13 UTC 2026
;; MSG SIZE  rcvd: 55

HTTP check: curl -I <http/https-url> — note the HTTP status code.
ubuntu@ip-172-31-16-85:~$ curl -I https://google.com
HTTP/2 301
location: https://www.google.com/
content-type: text/html; charset=UTF-8
content-security-policy-report-only: object-src 'none';base-uri 'self';script-src 'nonce--ARqnKOkPrOVY57UV8aemA' 'strict-dynamic' 'report-sample' 'unsafe-eval' 'unsafe-inline' https: http:;report-uri https://csp.withgoogle.com/csp/gws/other-hp
reporting-endpoints: default="//www.google.com/httpservice/retry/jserror?ei=P2ONaZf3OfSRm9cP04zMqQo&cad=crash&error=Page%20Crash&jsel=1"
date: Thu, 12 Feb 2026 05:21:03 GMT
expires: Sat, 14 Mar 2026 05:21:03 GMT
cache-control: public, max-age=2592000
server: gws
content-length: 220
x-xss-protection: 0
x-frame-options: SAMEORIGIN
alt-svc: h3=":443"; ma=2592000,h3-29=":443"; ma=2592000


Connections snapshot: netstat -an | head — count ESTABLISHED vs LISTEN (rough).
ubuntu@ip-172-31-16-85:~$ netstat -an | head
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address           Foreign Address         State
tcp        0      0 127.0.0.54:53           0.0.0.0:*               LISTEN
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN
tcp        0      0 127.0.0.53:53           0.0.0.0:*               LISTEN
tcp        0      0 172.31.16.85:54742      54.191.55.41:80         TIME_WAIT
tcp        0    516 172.31.16.85:22         157.49.21.68:58505      ESTABLISHED
tcp6       0      0 :::22                   :::*                    LISTEN
udp        0      0 127.0.0.1:323           0.0.0.0:*
udp        0      0 127.0.0.54:53           0.0.0.0:*
ubuntu@ip-172-31-16-85:~$

Pick one target service/host (e.g., google.com, your lab server, or a local service) and stick to it for ping/traceroute/curl where possible.


ubuntu@ip-172-31-16-85:~$ nc -zv localhost 22
Connection to localhost (127.0.0.1) 22 port [tcp/ssh] succeeded!
ubuntu@ip-172-31-16-85:~$ ^C
ubuntu@ip-172-31-16-85:~$

