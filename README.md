#  Penetration Testing Report – Mayo Industries

> A comprehensive penetration testing engagement conducted on **Mayo Industries**, covering external/internal network assessment, web application testing, and full Red-Blue-Purple team analysis.
>
> 📥 **[Click here to read the full report (PDF)](https://mysliit-my.sharepoint.com/:b:/g/personal/it23605398_my_sliit_lk/IQD-Q4hbdGnWRbq6lkviuR_ZAQb5nhbnTMYsQzLvSEWS1kU?e=kL1Uwv)**

---

## 📌 Overview

This report documents a structured penetration test performed against a simulated company network. The assessment follows a complete attack lifecycle — from reconnaissance to exploitation, privilege escalation, and lateral movement — paired with a defensive analysis and improvement validation.

The engagement was divided into three teams to simulate a realistic security assessment model:

| Team | Role |
|------|------|
| 🔴 **Red Team** | Simulated attacker — identified and exploited vulnerabilities |
| 🔵 **Blue Team** | Defender — analyzed detection capability and security controls |
| 🟣 **Purple Team** | Bridged both sides — identified gaps and validated improvements |

> 💡 *This report was originally created as a university assignment. Feel free to use it as a learning reference for penetration testing concepts and methodology.*

---

## 🧪 Lab Environment

| Machine | IP Address | Role |
|---|---|---|
| Kali Linux | 192.168.56.100 | Attacker Machine (Red Team Platform) |
| OWASP VM | 192.168.56.101 | Web/Application Server |
| Metasploitable 2 | 192.168.56.102 | Vulnerable Linux Server |
| Windows 7 | 192.168.56.103 | Internal Workstation |

---

## 🔴 Red Team – Offensive Assessment

The Red Team simulated real-world attacker behaviour across three assessment areas:

- **External Network Assessment** – Host discovery, port scanning, service enumeration, and vulnerability identification using tools like Nmap, Nikto, and Searchsploit.
- **Exploitation** – Successfully exploited `vsftpd 2.3.4` (FTP backdoor) and `distcc` (remote command execution) on Metasploitable 2 using Metasploit Framework.
- **Internal Enumeration** – Post-exploitation enumeration including user accounts, password hash extraction, and weak file permissions.
- **Privilege Escalation** – Abused a misconfigured SUID Nmap binary to escalate from `daemon` to `root`.
- **Lateral Movement** – Exploited the Windows 7 machine using the EternalBlue (MS17-010) exploit, achieving `NT AUTHORITY\SYSTEM` access.
- **Web Application Testing** – Tested the DVWA application for SQL Injection, Reflected XSS, and Brute Force vulnerabilities.

---

## 🔵 Blue Team – Defensive Analysis

The Blue Team evaluated the existing security controls against the Red Team's attacks:

- Analyzed Apache access and error logs (`/var/log/apache2/`)
- Found that SQL Injection and XSS attacks were **visible in logs** but triggered **no automated alerts**
- Brute Force attacks were **completely undetected**
- No IDS/IPS, EDR, or SIEM system was in place
- Incident handling capability was assessed as **weak** due to reliance on passive logging only

---

## 🟣 Purple Team – Gap Analysis & Validation

The Purple Team bridged the Red and Blue teams to identify security gaps and validate improvements:

| Attack | Before Fix | Improvement Applied | After Fix |
|---|---|---|---|
| SQL Injection | Data leaked | Input validation + parameterized queries | Blocked |
| XSS | Script executed | Input sanitization + output encoding | Blocked |
| Brute Force | Credentials cracked | Account lockout + strong passwords | Blocked |
| FTP Exploit (vsftpd) | Shell access gained | Service patched/disabled | Failed |
| distcc Exploit | Command execution | Service disabled | Failed |
| Privilege Escalation | Root access gained | SUID bit removed | Failed |
| Lateral Movement | SYSTEM access on Windows | Segmentation + SMB patched | Blocked |

---

## 📋 Key Vulnerabilities Found

| Vulnerability | Risk Level |
|---|---|
| vsftpd 2.3.4 Backdoor (FTP) | 🔴 Critical |
| distcc Remote Command Execution | 🔴 Critical |
| EternalBlue MS17-010 (SMB) | 🔴 Critical |
| SUID Nmap Privilege Escalation | 🔴 Critical |
| SQL Injection (DVWA) | 🟠 High |
| Apache 2.2.8 Misconfigurations | 🟠 High |
| Cross-Site Scripting (XSS) | 🟠 High |
| Weak Authentication / Brute Force | 🟠 High |
| Samba 3.0.20 (SMB Shares) | 🟠 High |

---

## 🛠️ Tools Used

`Nmap` · `Nikto` · `Metasploit Framework` · `Searchsploit` · `Hydra` · `Gobuster` · `WhatWeb` · `smbclient` · `John the Ripper` · `Burp Suite` · `Netcat`

---

## 📌 Disclaimer

> This report was created **solely for academic purposes** as part of the IE3022 coursework at SLIIT. All testing was performed in an **isolated virtual lab environment** with full permission. No real systems were targeted or harmed.

---


