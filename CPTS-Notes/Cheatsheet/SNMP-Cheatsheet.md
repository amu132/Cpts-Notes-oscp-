# SNMP Cheatsheet

## Enumeration
| Command | Use |
|---------|-----|
| `snmpwalk -v2c -c public <IP>` | Full OID tree dump |
| `snmpwalk -v2c -c <string> <IP> <OID>` | Specific OID query |
| `onesixtyone -c wordlist.txt <IP>` | Community string brute-force |
| `braa <string>@<IP>:.1.3.6.*` | OID brute-force |

## Default Community Strings to Try
| String |
|--------|
| public |
| private |
| community |

## Ports
| Port | Use |
|------|-----|
| 161/UDP | SNMP requests |
| 162/UDP | SNMP traps |
