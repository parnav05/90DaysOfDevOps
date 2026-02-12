Explain in 3–4 lines: what happens when you type google.com in a browser?
What are these record types? Write one line each:
A, AAAA, CNAME, MX, NS
Run: dig google.com — identify the A record and TTL from the output


DNS = Domain Name System
It converts:
google.com  →  142.250.183.14
Humans remember names.
Machines communicate using IP addresses.

what happens when you type google.com in a browser?

1️⃣ Browser Check (Local Cache)  Browser cache  OS cache (/etc/hosts) Local DNS cache
2️⃣ Query Goes to Recursive Resolver Public DNS like: Google Public DNS (8.8.8.8)
3️⃣ Root Server If resolver doesn’t know the answer:It asks a Root DNS Server:“Where is .com?” Root doesn’t give IP .It says:“Ask the .com TLD server.”
4️⃣ TLD Server (.com) Resolver now asks:“Where is google.com?”TLD replies:“Ask Google’s authoritative name server.”
5️⃣ Authoritative Name ServerThis is owned by Google.It replies:google.com = 142.250.183.14 Resolver caches it and sends back to you.


DNS Record Types (One Line Each)
A (Address Record)
Maps a domain name to an IPv4 address (e.g., example.com → 192.0.2.1).

AAAA (Quad-A Record)
Maps a domain name to an IPv6 address (e.g., example.com → 2001:db8::1).

CNAME (Canonical Name)
Creates an alias of one domain to another domain name (not directly to an IP).

MX (Mail Exchange)
Specifies the mail server responsible for receiving emails for a domain.

NS (Name Server)
Defines which authoritative DNS servers handle queries for the domain.

🧠 Quick Memory Trick

A → IPv4
AAAA → IPv6
CNAME → Alias
MX → Mail
NS → Name Server

Task 2: IP Addressing
What is an IPv4 address? How is it structured? (e.g., 192.168.1.10)
Difference between public and private IPs — give one example of each
What are the private IP ranges?
10.x.x.x, 172.16.x.x – 172.31.x.x, 192.168.x.x
Run: ip addr show — identify which of your IPs are private

What is an IPv4 Address?
An IPv4 address is a 32-bit logical address used to identify a device on a network.
Example:
192.168.1.10
It tells:
Who you are (your device)
Where you are (your network)
🧱 How is IPv4 Structured?
IPv4 = 32 bits
Divided into 4 octets
Each octet = 8 bits
Range per octet: 0–255
Example:
192.168.1.10
Binary form:
11000000.10101000.00000001.00001010
Structure generally:
Network Portion | Host Portion
Depending on subnet mask.
🌎 Public vs Private IP
🔵 Public IP
Globally unique
Routable on the internet
Assigned by ISP
Example:
8.8.8.8
(This belongs to Google Public DNS)
🟢 Private IP
Used inside local networks (LAN)
Not routable on internet directly
Used behind NAT
Example:
192.168.1.10
🔐 Private IP Ranges (Very Important)
These are reserved ranges:
1️⃣ 10.0.0.0 – 10.255.255.255
10.x.x.x
2️⃣ 172.16.0.0 – 172.31.255.255
172.16.x.x – 172.31.x.x
3️⃣ 192.168.0.0 – 192.168.255.255
192.168.x.x
Anything outside these = public (generally).
🖥 Now Run This:
ip addr show
You may see something like:
inet 192.168.1.25/24
inet 127.0.0.1/8
inet 10.0.2.15/24

🔎 Identify Private IP

Check if your IP falls into:

10.x.x.x → Private

172.16–31.x.x → Private

192.168.x.x → Private

Example:

192.168.1.25 → Private
10.0.2.15 → Private

What does /24 mean in 192.168.1.0/24?
How many usable hosts in a /24? A /16? A /28?
Explain in your own words: why do we subnet?
Quick exercise — fill in:
CIDR	Subnet Mask	Total IPs	Usable Hosts
/24	?	?	?
/16	?	?	?
/28	?	?	?


📘 1️⃣ CIDR Kya Hai?

CIDR = Classless Inter-Domain Routing

Pehle IP addresses classes me hote the:

Class A

Class B

Class C

CIDR ne class system hata diya aur flexible subnetting allow ki.

Example:

192.168.1.0/24


Yaha /24 ko kehte hain prefix length.

🧠 /24 Ka Matlab Kya?

IPv4 = 32 bits total.

/24 = first 24 bits network ke liye
Remaining 8 bits host ke liye


Mathematical:

2^(32 - 24) = 256 total IPs


Usme:

1 network address

1 broadcast address

254 usable hosts

🧱 CIDR Format
IP_Address / Prefix


Example:

10.0.0.0/8
172.16.0.0/16
192.168.1.0/24

📦 Common CIDR Examples
CIDR	Subnet Mask	Usable Hosts
/8	255.0.0.0	~16M
/16	255.255.0.0	65,534
/24	255.255.255.0	254
/30	255.255.255.252	2
2️⃣ Subnetting Kya Hai?

Subnetting ka matlab:

Ek bade network ko chhote networks me divide karna.

Example:

192.168.1.0/24


Isko split karte hain:

192.168.1.0/26


Now:

/26 = 64 IPs per subnet


256 ÷ 64 = 4 subnets

🔢 Example – /26 Breakdown

Original:

192.168.1.0/24


Subnet into /26:

192.168.1.0/26
192.168.1.64/26
192.168.1.128/26
192.168.1.192/26


Each subnet = 62 usable hosts.

🧠 Simple Formula
Total IPs = 2^(32 - prefix)
Usable = Total - 2


(Except /31 and /32 special case)



What is a Port?

A port is a logical communication endpoint on a system.

Simple language me:

IP batata hai kaunsa machine
Port batata hai machine ke andar kaunsi service

🧠 Why Do We Need Ports?

Ek server par multiple services chal sakti hain:

Web server

Database

SSH

DNS

Agar ports na hote, system ko pata hi nahi chalta kaunsi service ko traffic dena hai.

Example:

192.168.1.10:80


IP = Machine

Port 80 = Web server

🔥 Real Example

Socho:

IP = Apartment building

Port = Flat number

Service = Jo insaan us flat me rehta hai

📌 Common Ports (Documented)
Port	Service
22	SSH (Secure Shell)
80	HTTP (Web)
443	HTTPS (Secure Web)
53	DNS
3306	MySQL
6379	Redis
27017	MongoDB
🧠 Quick Explanation (One Line Each)
🔹 22 → SSH

Remote login and server management.

🔹 80 → HTTP

Unsecured web traffic.

🔹 443 → HTTPS

Encrypted web traffic (TLS/SSL).

🔹 53 → DNS

Domain name resolution.

🔹 3306 → MySQL

Database server port.

🔹 6379 → Redis

In-memory cache database.

🔹 27017 → MongoDB

NoSQL database service.