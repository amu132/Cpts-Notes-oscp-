# Enumeration Methodology

## What is it?
6-layer methodology for structured enumeration — external aur internal pentests ke liye.
3 levels: Infrastructure-based, Host-based, OS-based enumeration.

Methodology = systematic approach — step-by-step guide nahi hai.

## When to use?
Har pentest mein — chahe black-box ho ya white-box.
Structure follow karo — kuch miss na ho.

## 6 Layers

| Layer | Name | Goal | Key Info |
|-------|------|------|----------|
| 1 | Internet Presence | Sabhi targets identify karo | Domains, Subdomains, IPs, ASN, Cloud, vHosts |
| 2 | Gateway | Protection samjho | Firewalls, DMZ, IPS/IDS, EDR, Proxies, VPN |
| 3 | Accessible Services | Services aur functionality samjho | Service type, Port, Version, Config |
| 4 | Processes | Data flow samjho | PID, Tasks, Source, Destination |
| 5 | Privileges | Permissions identify karo | Users, Groups, Permissions, Restrictions |
| 6 | OS Setup | Internal system info nikalo | OS type, Patch level, Config files |

## 3 Enumeration Levels
- Infrastructure-based enumeration
- Host-based enumeration
- OS-based enumeration

## Key Concepts
- Labyrinth analogy — gaps/vulnerabilities = entry points
- Not all gaps lead inside — time wisely use karo
- Layer 1 aur 2 internal AD infrastructure pe apply nahi hote directly
- Is module mein mainly Layer 3 (Accessible Services) cover hoga

## My Lab Notes
- Methodology = framework, tools = cheatsheet — dono alag hain
- Brute-force se pehle enumeration complete karo
- SolarWinds attack example — months ki study = deeper understanding
- 4 week pentest mein bhi 100% vulnerabilities nahi milti — methodology isliye zaroori hai
- Dynamic process hai — har target alag hoga

## References
- HTB Module: Footprinting — Section 2 (Enumeration Methodology)

## MITRE
T1592 - Gather Victim Host Information
T1590 - Gather Victim Network Information
T1591 - Gather Victim Org Information
