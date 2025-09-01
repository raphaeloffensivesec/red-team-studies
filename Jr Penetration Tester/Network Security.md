# TryHackMe - Network Security (Jr Penetration Tester)

## 📌 Room Overview
- **Name:** Network Security  
- **Learning Path:** Jr Penetration Tester  
- **Difficulty:** Easy  
- **Tags:** Reconnaissance, Enumeration, Nmap, Networking, Penetration Testing  

This room introduces the **foundations of network reconnaissance, mapping, and enumeration**, teaching how attackers gather information about targets and how defenders can detect such activities.  
It focuses heavily on **Nmap** as the primary scanning tool, while also covering fundamental network discovery commands.  

---

## 1. 🔎 Introduction
Before exploiting vulnerabilities, attackers need to **understand the target network**. This process is split into:
- **Passive Reconnaissance:** Gathering info without touching the target directly (stealthy).
- **Active Reconnaissance:** Directly interacting with the target to extract information (noisier).

The main objective of this room is to gain skills in **host discovery, port scanning, service enumeration, and mapping network structures**.

---

## 2. 🕵 Reconnaissance Techniques

### 2.1 Passive Reconnaissance
- No direct interaction with target systems.  
- Examples:
  - Google Dorking
  - WHOIS Lookups
  - DNS Enumeration with public tools
  - Leaked metadata, social media analysis
- ✅ Advantage: Difficult to detect
- ❌ Disadvantage: Limited technical data

### 2.2 Active Reconnaissance
- Sending requests directly to the target.  
- Examples:
  - `ping`
  - `nmap`
  - `nc`
- ✅ Advantage: Provides accurate, real-time data
- ❌ Disadvantage: Creates logs and alerts in IDS/IPS systems

---

## 3. 🌐 Host Discovery & Mapping

### 3.1 ICMP Echo Request (Ping)
- Test if a host is alive.  
- Command: `ping <target-ip>`  
- Limitation: ICMP may be blocked by firewalls.

### 3.2 Traceroute
- Shows the path packets take across routers.  
- Useful for mapping infrastructure.  
- Linux command: `traceroute <target-ip>`  
- Windows command: `tracert <target-ip>`

### 3.3 ARP Scans
- Used in local networks to discover active hosts.  
- Command: `arp-scan -l`  
- Advantage: Bypasses ICMP/Firewall restrictions.

---

## 4. ⚡ Nmap Fundamentals

Nmap is the industry-standard tool for host and port discovery.

### 4.1 Basic Scan
- `nmap <target-ip>` → Performs a default scan of common ports.

### 4.2 Service and Version Detection
- `nmap -sV <target-ip>` → Identifies running services and their versions.

### 4.3 Script Scanning
- `nmap -sC <target-ip>` → Runs default scripts to extract extra data.

### 4.4 Aggressive Scan
- `nmap -A <target-ip>` → Includes OS detection, versioning, scripts, and traceroute. ⚠️ Very noisy, often detected.

### 4.5 Output Options
- `nmap -oN result.txt <target-ip>` → Normal text output  
- `nmap -oX result.xml <target-ip>` → XML format  
- `nmap -oG result.grep <target-ip>` → Greppable format  

---

## 5. 🚪 Port Scanning Techniques

### 5.1 TCP Connect Scan (-sT)
- Completes the full TCP handshake.  
- Reliable, but very noisy.

### 5.2 SYN Scan (-sS)
- Known as "half-open scan".  
- Faster, stealthier, harder to detect.  
- Requires root privileges.

### 5.3 UDP Scan (-sU)
- Checks UDP-based services (DNS, SNMP, DHCP, etc).  
- Slower, due to lack of responses in many cases.

### 5.4 Combined Scans
- Example: `nmap -sS -sV -p- -T4 <target-ip>` → Scans all ports, identifies services, and uses faster timing.

---

## 6. 🔍 Service Enumeration

After identifying open ports, the next step is to **enumerate the services**.

### 6.1 Banner Grabbing
- Extracts banners that reveal service versions.  
- Example: `nc <target-ip> 80`

### 6.2 Common Services
- **FTP (21):**  
  - Check for anonymous login with `ftp <target-ip>`  
- **SSH (22):**  
  - Banner may reveal software and version.  
- **HTTP (80/443):**  
  - Use `curl` or browser to check response.  
  - Run directory bruteforce with `gobuster dir -u http://<target-ip> -w <wordlist>`  
  - Inspect `robots.txt`, source code, hidden fields.  
- **SMB (139/445):**  
  - Enumerate shares: `smbclient -L //<target-ip>/`  
  - Test null sessions.  

---

## 7. 🧪 Practical Exercises from the Room
- Ping the host to confirm if alive.  
- Run multiple Nmap scans:  
  - Standard scan  
  - Service detection  
  - Script scanning  
  - Full port scan  
- Enumerate FTP, SMB, SSH, and HTTP services.  
- Compare results from **TCP Connect** vs **SYN** scans.  
- Perform **UDP scanning** to identify services missed in TCP.  

---

## 8. 📚 Lessons Learned
1. Reconnaissance is divided into **passive** and **active** approaches.  
2. **Nmap** is the most important tool for host discovery and enumeration.  
3. Each scan type has trade-offs between **stealth, speed, and completeness**.  
4. Service enumeration reveals potential attack vectors.  
5. Network defenders can detect noisy scans (connect/UDP) more easily than stealthy SYN scans.  

---

## 9. ⚠️ Disclaimer
All tests were performed inside **TryHackMe’s legal environment**.  
These techniques must **never be used against systems without explicit authorization**. Unauthorized scanning is illegal and unethical.

---
