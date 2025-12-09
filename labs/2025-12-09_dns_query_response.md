DNS Query & Response Analysis Lab (2025-12-09)
🔹 Objective

Analyze DNS request and response traffic using Wireshark to understand how domain names are resolved into IP addresses.

🖥️ Lab Environment

- Kali Linux VM
- Wireshark 4.x
- Internet connectivity enabled on eth0
- Interface configuration:
  - eth0 = bridged/NAT interface reaching DNS server
  - eth1 = internal network (not used here)

📌 Step-by-Step Instructions
1. Launch Wireshark

- Open Wireshark with root privileges:
  - sudo wireshark

- Select interface:
  - Choose eth0 (the interface with internet traffic)
  - Click Start Capturing

2. Apply a DNS Filter

- In the display filter bar, type:
  - dns
- This will show only DNS packets.

3. Generate DNS Traffic

- In a terminal, run:
  - ping -c 1 yahoo.com
- Or any domain you want to test.
- This forces your system to send:
  - DNS query → asking for yahoo.com’s IP
  - DNS response → DNS server replying with IP

4. Verify DNS Packets in Wireshark

- You should now see:
- DNS Query
  - Protocol: DNS
  - Info: Standard query A yahoo.com
  - Source: Your machine (ex: 10.0.2.3)
  - Destination: DNS server (ex: 10.0.2.16)
- DNS Response
  - Protocol: DNS
  - Info: Standard query response A yahoo.com A 74.6.x.x
  - Source: DNS server (10.0.2.16)
  - Destination: your machine (10.0.2.3)

📊 Packet Breakdown
- DNS Query Example
  - Transaction ID: 0x8c9e
  - Flags: Standard query
  - Questions: yahoo.com: type A
  - No answers yet (queries never have answers)
- DNS Response Example
  - Transaction ID: matches query
  - Answer RRs: 1+
  - Answer: A record — ex: yahoo.com → 74.6.231.20
  - Protocol: UDP port 53

🧠 What You Learned

- ✔ How DNS resolution works
- ✔ How to capture live DNS traffic
- ✔ How to filter and analyze DNS query/response
- ✔ How DNS maps domain names → IP addresses
- ✔ How to validate real traffic using Wireshark and terminal tools

🖼️ Screenshots
1. Wireshark DNS Query View

2. DNS Response Screenshot

3. Successful DNS Query/Response Filter

(Adjust screenshot filenames if needed to match what you uploaded.)

📁 Files for Submission

Wireshark capture file: eth0_dns_capture.pcapng (optional)

🎯 End of Lab

This lab demonstrates practical packet analysis skills used in SOC roles—DNS patterns are one of the most common signals analysts investigate.

## 📸 Screenshots

### 1. DNS Query and Ping
![DNS Query and Ping](../screenshots/dns_query_and_ping.png)

### 2. DNS Query Packet – Detailed View
![DNS Query Packet Details](../screenshots/wireshark_dns_query_view.png)

### 3. Filtered DNS Responses
![Filtered DNS Responses](../screenshots/dns_response_filtered_view.png)
