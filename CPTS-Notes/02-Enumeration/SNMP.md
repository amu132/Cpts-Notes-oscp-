# SNMP - Simple Network Management Protocol

## What is it?
SNMP = network devices monitor + manage karne ka protocol (routers, switches, IoT, servers).
UDP port 161 = normal communication (client → server request)
UDP port 162 = traps (server → client, unrequested event notifications)

Community strings = passwords jo access control karte hain.

## When to use?
Port 161/162 open mile toh.
Community string guess/brute-force karo (default: `public`, `private`).
Internal system info leak hota hai — usernames, software, OS details.

## SNMP Versions
| Version | Security |
|---------|----------|
| SNMPv1 | No authentication, no encryption — plaintext |
| SNMPv2c | Community-based, still plaintext |
| SNMPv3 | Username/password auth + encryption (pre-shared key) — most secure but complex |

## MIB & OID Concepts
- **MIB** = Management Information Base — text file, tree hierarchy of queryable objects
- **OID** = Object Identifier — unique dot-notation address (e.g. `.1.3.6.1.2.1.1.1.0`)
- Longer OID chain = more specific info

## Commands

```bash
# SNMPwalk — full OID tree query
snmpwalk -v2c -c public 10.129.14.128

# OneSixtyOne — community string brute-force
sudo apt install onesixtyone
onesixtyone -c /opt/useful/seclists/Discovery/SNMP/snmp.txt 10.129.14.128

# Braa — OID brute-force enumeration
sudo apt install braa
braa public@10.129.14.128:.1.3.6.*
```

## Dangerous Settings
| Setting | Risk |
|---------|------|
| `rwuser noauth` | Full OID tree access — no authentication! |
| `rwcommunity <string> <IP>` | Full OID tree access from anywhere (IPv4) |
| `rwcommunity6 <string> <IP>` | Same, IPv6 version |

## Key Config Files
| File | Use |
|------|-----|
| `/etc/snmp/snmpd.conf` | SNMP daemon config |

## What SNMP Leaks
- OS version, kernel details
- Installed software packages (Python, apt packages)
- Usernames/emails (sysContact field)
- System uptime, network interfaces
- Running processes

## My Lab Notes
- Default community strings try karo pehle: `public`, `private`
- `snmpwalk` sabse basic — pura data dump karta hai agar community string correct ho
- Community string unknown hai toh `onesixtyone` + SecLists wordlist use karo
- `braa` fast OID brute-force ke liye — bulk info nikalne mein useful
- sysContact field mein employee email/username milta hai — SMTP/user enum ke saath combine karo
- Installed packages list se vulnerable software versions identify ho sakte hain

## References
- HTB Module: Footprinting — SNMP Section
- SecLists: /opt/useful/seclists/Discovery/SNMP/
- Object Identifier Registry

## MITRE
T1046 - Network Service Discovery
T1082 - System Information Discovery
T1087 - Account Discovery
EOF
