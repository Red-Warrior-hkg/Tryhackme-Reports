<div align="center">

# 🥒 Pickle Rick — CTF Writeup

> 🧪 A structured penetration testing walkthrough of the **Pickle Rick** CTF room on TryHackMe —

> covering **enumeration**, **web exploitation**, and **privilege escalation** from zero to root.


---
### [**👉 Click Here to View the Full Report**](https://github.com/Red-Warrior-hkg/Tryhackme-Reports/blob/main/PickleRick/PickleRick_CTF_Report.pdf)
---

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
|🏷️ **Issued by**|RedWarrior|
|📅 **Date**|April 13 – 14, 2026|

---

## 🎯 Objectives

* 🔍 Practice real-world penetration testing methodology
* 🕸️ Understand common web vulnerabilities (info disclosure, credential leakage)
* ⚡ Demonstrate privilege escalation via `sudo` misconfiguration
* 📝 Produce a structured, professional CTF writeup

---

## 🚩 Flags Captured

|#|Location|Flag|
|-|-|-|
|🟢 **Flag 1**|`/var/www/html/Sup3rS3cretPickl3Ingred.txt`|`mr. meeseek hair`|
|🟡 **Flag 2**|`/home/rick/second ingredients`|`1 jerry tear`|
|🔴 **Flag 3**|`/root/3rd.txt`|`fleeb juice`|

---

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

---

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

---

## ⚠️ Key Vulnerabilities Found

|Vulnerability|Location|Severity|
|-|-|-|
|🔴 Credential leaked in HTML comment|`index.html` source|**High**|
|🔴 Password stored in `robots.txt`|`/robots.txt`|**High**|
|🔴 Unauthenticated OS command panel|`portal.php`|**Critical**|
|🔴 `sudo NOPASSWD: ALL` misconfiguration|`/etc/sudoers`|**Critical**|

---

## ⭐ Support

<div align="center">

If this writeup helped you — show some love!
---

> 📌 **Issued by RedWarrior** — Educational use only.
> This writeup is intended strictly for learning purposes within authorized CTF environments.

</div>

