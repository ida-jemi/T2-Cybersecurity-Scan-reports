<h1>🔐 Network Security & Scanning Lab</h1>

<h3>📌 Overview</h3>

This project demonstrates practical implementation of network security concepts including reconnaissance, port scanning, vulnerability assessment, packet analysis, and firewall configuration using industry-standard tools.

---

<h3>🎯 Objective</h3>

* Perform passive and active reconnaissance
* Scan target systems for open ports and services
* Identify vulnerabilities and analyze risk levels
* Capture and analyze network traffic
* Implement basic firewall rules

---

<h3>🧰 Tools Used</h3>

* Kali Linux
* Metasploitable2
* Nmap
* Wireshark
* OpenVAS (GVM)
* hping3
* iptables

---

<h3>🌐 Network Setup</h3>

| Machine        | IP Address     | Role     |
| -------------- | -------------- | -------- |
| Kali Linux     | 192.168.56.103 | Attacker |
| Metasploitable | 192.168.56.101 | Target   |

---

# 🕵️ 1. Reconnaissance

## 🔹 Passive Recon

Commands used:

```bash
whois example.com
nslookup example.com
```

## 🔹 Active Recon

### Ping Sweep

```bash
nmap -sn 192.168.56.0/24
```

### 📊 Result

* Identified live hosts in the network
* Confirmed target system availability

---

# 🔍 2. Port & Service Scanning

## 🔹 TCP SYN Scan

```bash
nmap -sS 192.168.56.101
```

## 🔹 Service Version Detection

```bash
nmap -sV 192.168.56.101
```

## 🔹 OS Detection

```bash
sudo nmap -O 192.168.56.101
```

---

<img width="752" height="645" alt="Screenshot 2026-04-13 231718" src="https://github.com/user-attachments/assets/07dcf841-d207-4d98-b899-ed1528520bbc" />

---

## 🔹 Full Scan

```bash
nmap -sS -sV -O -oN scan_report.txt 192.168.56.101
```

---

## 📊 Scan Results Summary

| Port | Service | Version      | Status |
| ---- | ------- | ------------ | ------ |
| 21   | FTP     | vsftpd 2.3.4 | Open   |
| 22   | SSH     | OpenSSH      | Open   |
| 23   | Telnet  | -            | Open   |
| 80   | HTTP    | Apache       | Open   |
| 139  | SMB     | Samba        | Open   |

---

## 🔎 Analysis

* Multiple unnecessary services are running
* Presence of outdated services increases risk
* FTP and Telnet are insecure (plaintext communication)

---

# 🛡️ 3. Vulnerability Scanning (OpenVAS)

## 🔹 Steps

1. Setup OpenVAS (GVM)
2. Created target: `192.168.56.101`
3. Configured scan (Full and Fast)
4. Executed vulnerability scan

---

<h3>📊 Results</h3>

| Severity    | Description                   |
| ----------- | ----------------------------- |
| 🔴 Critical | Backdoor vulnerability in FTP |
| 🟠 High     | Outdated Apache server        |
| 🟡 Medium   | Weak configurations           |
| 🟢 Low      | Informational findings        |

<img width="1919" height="1021" alt="Screenshot 2026-04-23 161357" src="https://github.com/user-attachments/assets/1d14e238-fd5b-44a6-8864-7735f06dcb5e" />

---

## 🔎 Analysis

* Critical vulnerabilities allow unauthorized access
* High-risk services require immediate patching
* Misconfigurations expose system to exploitation

<img width="1919" height="1019" alt="Screenshot 2026-04-23 161422" src="https://github.com/user-attachments/assets/6bbf5ba0-24f0-4fe6-b73e-85454dfcb9e4" />

---

# 📡 4. Packet Analysis (Wireshark)

## 🔹 Protocols Analyzed

* HTTP
* FTP
* DNS

<img width="1918" height="913" alt="image" src="https://github.com/user-attachments/assets/ce0fb592-30db-4853-84e7-2b06e014485b" />

---

## 🔹 Filters Used

```bash
http
ftp
dns
```

## 🔹 Credential Capture

```bash
ftp.request.command == "USER" || ftp.request.command == "PASS"
```

---

## 📊 Findings

* FTP credentials transmitted in plaintext
* HTTP traffic is unencrypted
* DNS queries visible

<img width="1847" height="868" alt="Screenshot 2026-04-17 145035" src="https://github.com/user-attachments/assets/7ac87534-6562-4a66-a7cc-a84d12ba9445" />

---

## 🔎 Analysis

* Lack of encryption leads to data exposure
* Sensitive information can be intercepted easily

---

# 🚨 5. SYN Flood Simulation

## 🔹 Command

```bash
sudo hping3 -S --flood -p 80 192.168.56.101
```

---

<img width="1838" height="840" alt="Screenshot 2026-04-17 144255" src="https://github.com/user-attachments/assets/17d99bab-0a37-4572-8517-999f5dff19f6" />

---

## 📊 Observation

* Large number of SYN packets detected in Wireshark
* Indicates potential DoS attack

---

# 🔥 6. Firewall Configuration

## 🔹 Block Port 80

```bash
sudo iptables -A INPUT -p tcp --dport 80 -j DROP
```

---

<img width="1047" height="738" alt="Screenshot 2026-04-17 150120" src="https://github.com/user-attachments/assets/246981fc-bd4e-40c5-984d-77e4ae700c26" />

---

## 🔹 Allow SSH

```bash
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
```

## 🔹 Verify Rules

```bash
sudo iptables -L
```

## 📊 Result

* Port 80 filtered after applying firewall rule
* Improved system security

---

# 🧠 Key Learnings

* Importance of reconnaissance in cybersecurity
* Identifying open ports and vulnerable services
* Real-world impact of unencrypted communication
* Basics of network attack detection
* Role of firewalls in securing systems

---

<h3>✅ Conclusion</h3>

This lab successfully demonstrated how attackers identify vulnerabilities and how defensive mechanisms like firewalls and monitoring tools help secure systems.

---
