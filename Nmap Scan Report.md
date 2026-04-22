<h1>🔍 Nmap Scan Report</h1>

## 📌 Overview

This report presents the results of network scanning performed on the target system to identify open ports, running services, and potential security risks.

---

## 🎯 Objective

* Identify active hosts in the network
* Detect open ports and services
* Determine service versions
* Identify operating system details

---

## 🌐 Target Information

| Parameter        | Value              |
|------------------|-------------------|
| Target IP        | 192.168.56.101    |
| Scanner Machine  | Kali Linux        |
| Tool Used        | Nmap              |

---

## ⚙️ Scan Commands Used

```bash
nmap -sS 192.168.56.101
nmap -sV 192.168.56.101
sudo nmap -O 192.168.56.101
nmap -sS -sV -O -oN scan_report.txt 192.168.56.101
```
---

<img width="641" height="546" alt="Screenshot 2026-04-13 231632" src="https://github.com/user-attachments/assets/31cc9530-0e07-4559-aace-89915ef126ad" />

---

<img width="1012" height="610" alt="Screenshot 2026-04-13 231701" src="https://github.com/user-attachments/assets/b38d8497-ccc8-4cb8-a5d6-519308578ac5" />

---

<img width="752" height="645" alt="Screenshot 2026-04-13 231718" src="https://github.com/user-attachments/assets/9bdd79f8-4602-4d86-985d-1e25ef0f1b33" />

---

<img width="1638" height="381" alt="Screenshot 2026-04-13 231849" src="https://github.com/user-attachments/assets/f5477736-fce8-4aed-8647-e6d081fc261f" />
