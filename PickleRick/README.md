<div align="center">

# 🥒 Pickle Rick — CTF Writeup

<br/>

[!\[Platform](https://img.shields.io/badge/Platform-TryHackMe-212C42?style=for-the-badge\&logo=tryhackme\&logoColor=white)](https://tryhackme.com/room/picklerick)
[!\[License](https://img.shields.io/badge/License-Educational-22c55e?style=for-the-badge\&logo=bookstack\&logoColor=white)](#)
[!\[Status](https://img.shields.io/badge/Status-Completed-a3e635?style=for-the-badge\&logo=checkmarx\&logoColor=white)](#)
[!\[Difficulty](https://img.shields.io/badge/Difficulty-Easy-f59e0b?style=for-the-badge\&logo=condaforge\&logoColor=white)](#)
[!\[Issued by](https://img.shields.io/badge/Issued%20by-RedWarrior-dc2626?style=for-the-badge\&logo=hackthebox\&logoColor=white)](#)

<br/>

[!\[Stars](https://img.shields.io/github/stars/<your-username>/<repo-name>?style=social)](https://github.com/<your-username>/<repo-name>)
[!\[Forks](https://img.shields.io/github/forks/<your-username>/<repo-name>?style=social)](https://github.com/<your-username>/<repo-name>/fork)

<br/>

> 🧪 A structured penetration testing walkthrough of the \*\*Pickle Rick\*\* CTF room on TryHackMe —
> covering \*\*enumeration\*\*, \*\*web exploitation\*\*, and \*\*privilege escalation\*\* from zero to root.

<br/>

\---

📄 **Want the full detailed report?**

### [**👉 Click Here to View the Full Report**](#) *(replace `#` with your report URL)*

\---

</div>

## 📖 Overview

This repository documents a **complete security assessment** of the *Pickle Rick* CTF challenge on TryHackMe.

The engagement follows a real-world penetration testing methodology:

```
Reconnaissance  →  Enumeration  →  Exploitation  →  Privilege Escalation  →  Root
```

|Field|Details|
|-|-|
|🎯 **Target**|Pickle Rick — TryHackMe|
|🌐 **Target IP**|`10.130.165.180`|
|🏆 **Points Earned**|`90`|
|🔑 **Flags Found**|`3 / 3`|
|👤 **Author**|vhmedx10|
|🏷️ **Issued by**|RedWarrior|
|📅 **Date**|April 13 – 14, 2026|

\---

## 🎯 Objectives

* 🔍 Practice real-world penetration testing methodology
* 🕸️ Understand common web vulnerabilities (info disclosure, credential leakage)
* ⚡ Demonstrate privilege escalation via `sudo` misconfiguration
* 📝 Produce a structured, professional CTF writeup

\---

## 🚩 Flags Captured

|#|Location|Flag|
|-|-|-|
|🟢 **Flag 1**|`/var/www/html/Sup3rS3cretPickl3Ingred.txt`|`mr. meeseek hair`|
|🟡 **Flag 2**|`/home/rick/second ingredients`|`1 jerry tear`|
|🔴 **Flag 3**|`/root/3rd.txt`|`fleeb juice`|

\---

## 📚 Quick Reference — Commands

```bash
# ── Reconnaissance ──────────────────────────────────────────────
# Full service \& OS detection
nmap -A <IP>

# HTTP path enumeration
nmap -p80,443 --script=http-enum <IP>

# ── Enumeration ─────────────────────────────────────────────────
# Directory brute-force
gobuster dir -u http://<IP> -w /usr/share/wordlists/dirb/common.txt

# Check robots.txt for hidden info
curl http://<IP>/robots.txt

# ── Exploitation ────────────────────────────────────────────────
# Read file when cat is blocked
strings <filename>

# Alternative file reader (also bypasses cat restriction)
less <filename>

# ── Privilege Escalation ────────────────────────────────────────
# Check sudo permissions
sudo -l

# List root directory as www-data (if NOPASSWD: ALL)
sudo ls -la /root

# Read root flag
sudo less /root/3rd.txt
```

\---

## ⚙️ Attack Flow

```
┌──────────────────────────────────────────────────────┐
│                  PICKLE RICK CTF                     │
└──────────────────────┬───────────────────────────────┘
                       │
              ┌────────▼────────┐
              │   RECON         │  Page source → username in HTML comment
              └────────┬────────┘
                       │
              ┌────────▼────────┐
              │  ENUMERATION    │  Gobuster + Nmap http-enum → /login.php
              └────────┬────────┘
                       │
              ┌────────▼────────┐
              │  CREDENTIALS    │  robots.txt → password discovered
              └────────┬────────┘
                       │
              ┌────────▼────────┐
              │  EXPLOITATION   │  Login → command panel → flags 1 \& 2
              └────────┬────────┘
                       │
              ┌────────▼────────┐
              │   PRIV ESC      │  sudo NOPASSWD:ALL → root → flag 3
              └─────────────────┘
```

\---

## ⚠️ Key Vulnerabilities Found

|Vulnerability|Location|Severity|
|-|-|-|
|🔴 Credential leaked in HTML comment|`index.html` source|**High**|
|🔴 Password stored in `robots.txt`|`/robots.txt`|**High**|
|🔴 Unauthenticated OS command panel|`portal.php`|**Critical**|
|🔴 `sudo NOPASSWD: ALL` misconfiguration|`/etc/sudoers`|**Critical**|

\---

## 🔮 Future Improvements

* \[ ] Automate recon script for similar CTF rooms
* \[ ] Include reverse shell escalation as an alternative path
* \[ ] Add CVSS scores for each vulnerability

\---

## ⭐ Support

<div align="center">

If this writeup helped you — show some love!

[!\[Star](https://img.shields.io/badge/⭐%20Star%20this%20Repo-a3e635?style=for-the-badge)](https://github.com/<your-username>/<repo-name>)
[!\[Share](https://img.shields.io/badge/📢%20Share%20It-f59e0b?style=for-the-badge)](#)
[!\[TryHackMe](https://img.shields.io/badge/🧠%20Follow%20on%20TryHackMe-212C42?style=for-the-badge)](https://tryhackme.com/p/vhmedx10)

<br/>

> 📌 \*\*Issued by RedWarrior\*\* — Educational use only.
> This writeup is intended strictly for learning purposes within authorized CTF environments.

</div>

