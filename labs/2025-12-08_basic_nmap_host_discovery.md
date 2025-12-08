# Lab: Basic Nmap Host Discovery & Port Scanning  
**Date:** 2025-12-08  
**Category:** Network Scanning / SOC Fundamentals  

---

## 📝 Overview  
This lab focuses on discovering active hosts on a network and identifying open ports using Nmap.  
I scanned my Kali Linux machine within a VirtualBox NAT network, enabled the SSH service, and observed how service exposure changes scan results.

---

## 🎯 Objectives  
- Perform a network host discovery using `-sn`  
- Identify open, closed, and filtered port states  
- Enable a service and observe how it appears in a scan  
- Use `-sV` for service version detection  
- Interpret results from a defender’s perspective  

---

## 🛠 Tools Used  
- **Kali Linux**  
- **Nmap 7.95**  
- **systemctl** (to manage SSH service)

---

## 🌐 Network Information  
Active interface: `eth0`  
IP Address: 10.0.2.16
Gateway: 10.0.2.2
Network: 10.0.2.0/24


---

## 🔎 Steps Performed  

### **1. Verified Network Connectivity**

ping -c 4 10.0.2.2

2. Discovered Hosts on the Network
sudo nmap -sn 10.0.2.0/24
Result:
Three hosts detected:
- 10.0.2.2 – NAT gateway
- 10.0.2.3 – VirtualBox internal host
- 10.0.2.16 – My Kali VM

3. Scanned My Kali VM (Initial Scan)
~ sudo nmap 10.0.2.16
Result:
All ports closed (no active services).

4. Enabled the SSH Service
~ sudo systemctl start ssh
~ sudo systemctl status ssh
SSH now listening on port 22.

5. Re-scanned After Enabling SSH
~ sudo nmap 10.0.2.16
Result:
22/tcp open ssh

6. Performed Service Version Detection
https://github.com/beefychipmunky/daily_cyber_labs/blob/main/labs/screenshots/nmap_sV_scan.png?raw=true
~ sudo nmap -sV 10.0.2.16
Result:
OpenSSH 10.0p2 Debian 5 (protocol 2.0)

📌 Findings
- Enabling SSH immediately exposed port 22 to Nmap scans.
- Version detection (-sV) revealed detailed software info.
- The small NAT network contained only VirtualBox management hosts.

💡 What I Learned
- How host discovery works at the network level
- How to interpret Nmap output (open/closed/filtered)
- How enabling a service changes a machine’s attack surface
- How attackers identify potential entry points
- How defenders validate service exposure and configuration

🛡 Real-World Relevance
Nmap is used daily for:
- SOC investigations
- Vulnerability scanning
- Asset inventory
- Exposure management
- Penetration testing reconnaissance
Understanding how to read and generate these scan results is a foundational cybersecurity skill.

📂 Screenshots
(Placeholder — adding screenshots soon)

✔ Status
Completed: 2025-12-08
