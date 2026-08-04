# 🛡️ 90 Days to Ethical Hacker — DAY 1
## Topic: How Computers & the Internet Actually Work (The Foundation)

> "You can't hack what you don't understand." Before we touch Kali Linux or Metasploit, we need rock-solid basics. Every pro pentester started exactly here.

---

## 1. 🎯 Learning Objectives

By the end of today, you will be able to:
- Explain what a computer actually *does* at a basic level
- Explain what the Internet is (and what it is NOT)
- Understand clients, servers, and requests/responses
- Understand what an IP address and a MAC address are
- Understand the idea of "ports" as doors into a computer
- Run your first basic commands in a terminal

---

## 2. 📖 Beginner-Friendly Theory

### What is a computer, really?
A computer is a machine that follows instructions (called **programs**) to move, store, and change data (1s and 0s — called **binary**). That's it. Everything — Windows, your phone, a website — is just instructions being followed very, very fast.

**Term explained:**
- **Data** = any information (a photo, a password, a webpage) stored as 1s and 0s.
- **Program/Software** = a list of instructions telling the computer what to do with data.
- **Hardware** = the physical parts (CPU, RAM, hard disk, network card).

### What is the Internet?
The Internet is a **giant network of networks** — millions of computers connected together so they can send messages to each other.

**Analogy 🏠📬:** Think of the Internet like the global postal system.
- Every house (computer) has an **address** (IP address).
- When you send a letter (data), it passes through local post offices (routers) until it reaches the right house.
- The letter has to be in an agreed format so the postal workers understand it (a **protocol**).

### Client vs Server
- **Client** = the one who *asks* for something (your laptop, your phone browser).
- **Server** = the one who *has* the thing and answers the request (a computer that stores a website, YouTube, etc.)

```
ASCII DIAGRAM: Client-Server Model
-----------------------------------

   [ YOU / CLIENT ]                     [ SERVER ]
   Laptop with Browser                  Computer storing website
        |                                     |
        |   1. "Please send me                |
        |       google.com's homepage"        |
        |------------------------------------>|
        |                                     |
        |   2. "Here is the webpage!"         |
        |<------------------------------------|
        |                                     |
   [ Browser shows page ]              [ Waits for next request ]
```

This "ask and answer" pattern is called a **Request/Response** model. Nearly ALL hacking of web apps (which you'll learn in Week 8) is about tampering with this request or response.

### IP Address — The House Address of the Internet
An **IP Address** is a unique number that identifies a device on a network.

Example: `192.168.1.10`

**Analogy:** It's like your home's street address — so data knows where to be delivered.

There are two types:
- **Public IP** — your address as seen from the whole Internet (like your city + house number seen by the whole world)
- **Private IP** — your address only inside your home/office network (only your family sees "Room 2's door")

```
ASCII DIAGRAM: Public vs Private IP
------------------------------------

        THE INTERNET (Public World)
                  |
          [ Public IP: 103.24.55.9 ]
                  |
             [ Your Router ]
             /      |       \
   [Laptop]     [Phone]    [Smart TV]
  192.168.1.5  192.168.1.6  192.168.1.7
   (Private IPs - only visible inside your home network)
```

### MAC Address — The Permanent ID Card
A **MAC Address** is a unique physical ID burned into your network card by the manufacturer, e.g. `A4:5E:60:11:22:33`. 

**Analogy:** If IP address is your *changeable home address*, MAC address is like your *fingerprint* — unique to the device, rarely changes.

### Ports — Doors Into a Computer
A computer doesn't just have ONE address — it has thousands of "doors" called **ports**, each used for a different type of service.

**Analogy 🏢:** Think of a computer as an office building (the IP address is the building's street address). Each port is a specific door/room number for a specific department:
- Port 80 = "Reception desk for normal website visitors" (HTTP)
- Port 443 = "Reception desk for secure website visitors" (HTTPS)
- Port 22 = "Staff-only maintenance entrance" (SSH — remote login)
- Port 21 = "File delivery dock" (FTP — file transfer)

```
ASCII DIAGRAM: A Computer's Ports
-----------------------------------
        IP Address: 192.168.1.10
    +-------------------------------+
    |         COMPUTER              |
    |  Port 21  -> FTP (files)      |
    |  Port 22  -> SSH (remote login)|
    |  Port 80  -> HTTP (website)   |
    |  Port 443 -> HTTPS (secure)   |
    |  Port 3389-> RDP (remote desk)|
    +-------------------------------+
```

This matters HUGELY in hacking — one of the first things a pentester does is **scan ports** to see which "doors" are open (we'll do this in Week 6 with Nmap).

---

## 3. 💡 Why It Matters (In Security Terms)

Every hack, at its core, exploits how computers communicate. If you understand:
- How requests/responses work → you'll understand web hacking (SQLi, XSS)
- How IP/ports work → you'll understand network scanning & exploitation
- How data travels → you'll understand sniffing (Wireshark) and man-in-the-middle attacks

**You cannot break something safely and skillfully if you don't first understand how it's built.**

---

## 4. 🌍 Real-World Example

When you type `www.google.com` in your browser:
1. Your computer asks "what's the IP address for google.com?" (this is called **DNS lookup** — we cover this Day 5)
2. It gets back an IP like `142.250.190.14`
3. Your browser sends an HTTP request to port 443 (HTTPS) at that IP
4. Google's server sends back the webpage
5. Your browser displays it

Attackers who understand this flow can intercept step 1 (DNS spoofing) or step 3-4 (man-in-the-middle) — but that's advanced stuff for later weeks. Today, just understand the *flow*.

---

## 5. 🖼️ Visual Explanation — Full Picture

```
     YOU TYPE: www.example.com
              |
              v
   +---------------------+
   |   DNS LOOKUP         |   "What's the IP for example.com?"
   |   (like a phonebook)  |
   +---------------------+
              |
              v
     IP found: 93.184.216.34
              |
              v
   +---------------------------+
   | Browser sends REQUEST      |
   | to 93.184.216.34 : Port 443|
   +---------------------------+
              |
              v
   +---------------------------+
   |  Server sends RESPONSE     |
   |  (the webpage HTML)        |
   +---------------------------+
              |
              v
      Browser renders the page
```

---

## 6. ⌨️ Commands Explained Line-by-Line

Open a terminal (Linux/Mac: Terminal app, Windows: press `Win+R`, type `cmd`, hit Enter).

### Command 1: Check your own IP address
```bash
# Linux/Mac
ip addr show

# Windows
ipconfig
```
**What this does, line by line:**
- `ip` → the base networking tool command in Linux
- `addr` → tells `ip` we want address information
- `show` → display it
- On Windows, `ipconfig` alone does the equivalent job.

**Expected Output (example):**
```
inet 192.168.1.15/24 brd 192.168.1.255 scope global
```
This means your private IP is `192.168.1.15`.

### Command 2: Ping a website (test if it's reachable)
```bash
ping google.com
```
**Explained:**
- `ping` → sends small test messages to a destination and waits for a reply — like shouting "Are you there?" and listening for an echo.
- `google.com` → the destination

**Expected Output:**
```
64 bytes from 142.250.190.14: icmp_seq=1 ttl=117 time=12.3 ms
```
This means Google replied in 12.3 milliseconds — the connection works!

**Troubleshooting:** If you see "Request timed out" — either you have no internet, or that server blocks pings (many servers do, for security reasons — we'll learn why later).

---

## 7. 🐧 Linux Basics (Today's Dose)

Since Linux is the hacker's main operating system, here are your first 5 commands:

| Command | What it does | Analogy |
|---|---|---|
| `pwd` | Print current folder location | "Where am I standing right now?" |
| `ls` | List files in current folder | "What's in this room?" |
| `cd foldername` | Move into a folder | "Walk into that room" |
| `whoami` | Show your username | "What's my name badge say?" |
| `clear` | Clear the terminal screen | "Wipe the whiteboard" |

**Practice this now:**
```bash
pwd
ls
whoami
```

---

## 8. 🌐 Networking Concepts Covered Today
- IP Address (public vs private)
- MAC Address
- Ports
- Client-Server model
- Basic request/response

*(Deep dive into OSI Model and TCP/IP comes Day 2-3)*

---

## 9. 🔐 Security Concepts Introduced
- Why understanding communication flow = foundation of hacking
- The idea that every "door" (port) is a potential entry point
- Why servers may block pings (early intro to defensive thinking)

---

## 10. 🎬 Demonstration

Let's demonstrate finding your own network info and testing connectivity.

**Step-by-step:**
1. Open terminal
2. Run `ip addr show` (Linux/Mac) or `ipconfig` (Windows) → note your private IP
3. Run `ping 8.8.8.8` → this is Google's public DNS server, great for testing raw connectivity
4. Run `ping google.com` → this tests both DNS AND connectivity

**Expected output difference:** If step 3 works but step 4 fails, your DNS (the "phonebook") has a problem, not your internet connection. This is real diagnostic thinking pentesters use daily!

---

## 11. 🧪 Practical Lab (Do This Now)

**Lab: Map Your Own Network**

1. Find your private IP address (`ip addr` / `ipconfig`)
2. Find your public IP address by visiting: https://whatismyipaddress.com (free, safe, legal — it's YOUR info)
3. Ping 3 different websites: `ping google.com`, `ping wikipedia.org`, `ping github.com`
4. Write down all 5 pieces of information in a notes file: private IP, public IP, and the 3 ping results (average time in ms)

**No special tools needed — just your regular computer.**

---

## 12. 📝 Walkthrough (Answer Key / Explanation)

- Your **private IP** will look like `192.168.x.x` or `10.0.x.x`
- Your **public IP** will be a totally different number — that's the address the whole internet sees you as
- Ping times under 50ms = fast connection; 50-150ms = normal; 150ms+ = slower/far server

If you got stuck: the most common issue is firewall/antivirus blocking ping — that's normal and expected on some networks (e.g., corporate WiFi).

---

## 13. 🏆 Challenge Lab

**Challenge:** Without me telling you, figure out:
1. What is the difference in ping time between `ping google.com` and `ping 8.8.8.8`? Why might they differ?
2. Try `ping` on a website that does NOT reply (hint: try `ping facebook.com`). Why do you think some companies block ping requests? (Think defensively — what could an attacker learn from ping responses?)

---

## 14. 🛠️ Mini Project

**Project: "My Network Fact Sheet"**

Create a text file called `network_notes.txt` containing:
```
My Private IP: ___________
My Public IP: ___________
My MAC Address: ___________ (find with 'ip addr' on Linux/Mac or 'getmac' on Windows)
3 Websites Pinged & Their Average Response Time:
1. ___________
2. ___________
3. ___________
```
Keep this file — we'll build on it as our course progresses!

---

## 15. ❓ Quiz (10 Questions)

1. What does "IP" stand for?
2. True/False: A MAC address can easily change every time you connect to WiFi.
3. What is the role of a "client" in the client-server model?
4. Name one port number and what service it's commonly used for.
5. What command shows your IP address on Linux?
6. What does the `ping` command actually do?
7. What is the difference between a public and a private IP address?
8. In the postal analogy, what represents a "protocol"?
9. What does DNS stand for (research this — hint word: "Domain")?
10. Why does understanding networking basics matter for ethical hacking?

*(Answers at the end of this document)*

---

## 16. 💼 Interview Questions

1. Explain the client-server model in your own words.
2. What's the difference between a public and private IP address?
3. What is a MAC address and how is it different from an IP address?
4. Why do ethical hackers need strong networking fundamentals?
5. What tool would you use to test if a remote host is reachable, and how does it work?

---

## 17. ⚠️ Common Mistakes (Beginners Make These!)

- Confusing IP address with MAC address (IP can change, MAC usually doesn't)
- Assuming "ping failed" always means "no internet" (often it's just a firewall blocking it)
- Thinking the Internet = the Web (the Web is just ONE service that runs ON the Internet; email, gaming, etc. are others)
- Skipping fundamentals to jump straight to "hacking tools" — this always backfires later

---

## 18. 📋 Cheatsheet

```
COMMAND                  PURPOSE
------------------------------------------
ip addr show             Show your IP (Linux/Mac)
ipconfig                 Show your IP (Windows)
ping <target>             Test connectivity
whoami                   Show current username
pwd                       Show current directory
ls / dir                  List files
cd <folder>               Change directory

KEY TERMS
------------------------------------------
IP Address    = Device's network address (can change)
MAC Address   = Device's physical hardware ID (rarely changes)
Port          = A numbered "door" for a specific service
Client        = Requests information
Server        = Provides information
Protocol      = Agreed set of communication rules
```

---

## 19. 📚 Homework

1. Complete the Mini Project (network_notes.txt)
2. Read (free): "How DNS Works" comic — https://howdns.works
3. Watch (free, optional): Any beginner "How the Internet Works" video on YouTube from Computerphile or PowerCert
4. Come back tomorrow ready for: **OSI Model & TCP/IP** (this is the single most important theory topic in networking — don't skip Day 2!)

---

## 20. 🔁 Revision Notes (Quick Recap)

- Computers run instructions on binary data
- The Internet = network of networks, connected globally
- Client asks, Server answers (Request/Response)
- IP Address = network "home address" (public = world-visible, private = local only)
- MAC Address = permanent hardware fingerprint
- Ports = doors into a computer for different services
- `ping` tests reachability; `ip addr`/`ipconfig` shows your address

---

## 📎 Free Resources for Today
- How DNS Works (comic): https://howdns.works
- Cisco Networking Basics (free): https://www.netacad.com
- Professor Messer Networking videos (free, YouTube)
- OWASP homepage (bookmark for later): https://owasp.org

---

## ✅ Quiz Answers
1. Internet Protocol
2. False — MAC addresses are largely fixed (hardware-assigned), though some devices use "randomized MAC" for privacy
3. The client is the one requesting a service/data
4. Port 80 = HTTP, Port 443 = HTTPS, Port 22 = SSH, Port 21 = FTP (any one correct)
5. `ip addr show`
6. Sends a small test message and measures if/how fast a reply comes back
7. Public = visible to the whole internet; Private = visible only inside your local network
8. The protocol = the agreed language/format the letter and postal system follow (e.g., how HTTP formats a web request)
9. Domain Name System
10. Because nearly every hacking technique exploits or manipulates how computers communicate over networks

---

# 🔮 Tomorrow Preview: Day 2
**Topic: The OSI Model & TCP/IP — The "7 Layers" That Run the Entire Internet**
We'll break down exactly how data travels from your keyboard to a server and back, layer by layer, with a full ASCII diagram. This is THE most asked topic in cybersecurity interviews — you'll want to be sharp for it!

Great work today. See you tomorrow. 💪
