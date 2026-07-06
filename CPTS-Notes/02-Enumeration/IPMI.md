# IPMI - Intelligent Platform Management Interface

## What is it?
IPMI = hardware-based host management, OS/BIOS/CPU se independent.
Powered-off ya unresponsive systems bhi manage/monitor kar sakte ho.
BMC (Baseboard Management Controller) = IPMI ka core micro-controller.

Common uses:
- BIOS settings modify (pre-boot)
- Powered-down host access
- System failure ke baad access
- Temperature, voltage, fan, power monitoring

## When to use?
Port 623/UDP open mile toh — internal pentest mein bahut common.
Default credentials try karo — sabse pehle.
Password mile toh — password reuse check karo across other systems (SSH, web consoles).

## Common BMC Implementations
| BMC | Vendor |
|-----|--------|
| HP iLO | Hewlett Packard |
| Dell DRAC | Dell |
| Supermicro IPMI | Supermicro |

BMC access = physical access ke barabar — reboot, power off, OS reinstall sab possible!

## Commands

# Nmap IPMI version scan
sudo nmap -sU --script ipmi-version -p 623 ilo.inlanfreight.local

# Metasploit — version scan
msf6 > use auxiliary/scanner/ipmi/ipmi_version
msf6 auxiliary(scanner/ipmi/ipmi_version) > set rhosts 10.129.42.195
msf6 auxiliary(scanner/ipmi/ipmi_version) > run

# Metasploit — dump password hashes (RAKP vulnerability)
msf6 > use auxiliary/scanner/ipmi/ipmi_dumphashes
msf6 auxiliary(scanner/ipmi/ipmi_dumphashes) > set rhosts 10.129.42.195
msf6 auxiliary(scanner/ipmi/ipmi_dumphashes) > run

# Hashcat — crack IPMI hash (mode 7300)
hashcat -m 7300 ipmi.txt -a 3 ?1?1?1?1?1?1?1?1 -1 ?d?u

## Default Credentials to Try
| Product | Username | Password |
|---------|----------|----------|
| Dell iDRAC | root | calvin |
| HP iLO | Administrator | Randomized 8-char (numbers + uppercase) |
| Supermicro IPMI | ADMIN | ADMIN |

## Key Vulnerability — RAKP Protocol Flaw (IPMI 2.0)
- Server salted SHA1/MD5 password hash bhejta hai client ko authentication SE PEHLE
- Kisi bhi valid user ka password hash retrieve ho sakta hai — bina login kiye!
- Offline crack karo Hashcat mode 7300 se
- No direct fix — critical IPMI spec ka part hai (design flaw)

## Required IPMI Components
| Component | Function |
|-----------|----------|
| BMC | Micro-controller — core of IPMI |
| ICMB | Chassis-to-chassis communication |
| IPMB | BMC extend karta hai |
| IPMI Memory | System event log, repository data store |

## My Lab Notes
- Port 623/UDP hamesha check karo internal pentests mein — bahut ignore hota hai
- Default creds try karna zaroori — sysadmins often change nahi karte
- RAKP flaw se hash mil jaaye toh Hashcat se crack karo — even weak/unique passwords crackable hote hain
- Cracked IPMI password bahut baar dusre systems pe reuse hoti hai — SSH try karo root ke saath
- BMC access = near-physical access — high-risk finding hamesha report karo
- IPMI checking = internal pentest playbook ka mandatory part

## References
- HTB Module: Footprinting — IPMI Section
- Metasploit ipmi_dumphashes module

## MITRE
T1046 - Network Service Discovery
T1110.002 - Brute Force: Password Cracking
T1078 - Valid Accounts
T1552 - Unsecured Credentials
