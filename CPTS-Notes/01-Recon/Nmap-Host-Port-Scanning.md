# Nmap - Host and Port Scanning

## What is it?
Port scan se pata karta hai — open ports, services, versions, OS.
Host discovery ke baad ka next step.

6 port states hote hain:

| State | Meaning |
|-------|---------|
| open | Connection established |
| closed | RST flag mila — port band hai |
| filtered | No response — firewall block kar raha hai |
| unfiltered | TCP-ACK scan mein — accessible but open/closed pata nahi |
| open\|filtered | No response — firewall ya filter ho sakta hai |
| closed\|filtered | IP ID idle scan mein — closed ya filtered pata nahi |

## When to use?
Host discovery ke baad — live hosts pe open ports aur services identify karne ke liye.
Service versions nikalne ke liye (-sV).

## Commands

```bash
# Top 10 TCP ports scan
sudo nmap 10.129.2.28 --top-ports=10

# SYN scan (default, stealthy, root required)
sudo nmap 10.129.2.28 -sS

# TCP Connect scan (full handshake, no root needed)
sudo nmap 10.129.2.28 -p 443 -sT

# Specific ports
sudo nmap 10.129.2.28 -p 22,80,443

# Port range
sudo nmap 10.129.2.28 -p 22-445

# All ports
sudo nmap 10.129.2.28 -p-

# Fast scan — top 100 ports
sudo nmap 10.129.2.28 -F

# UDP scan
sudo nmap 10.129.2.28 -F -sU

# UDP specific port with reason
sudo nmap 10.129.2.28 -sU -Pn -n --disable-arp-ping --packet-trace -p 137 --reason

# Version scan
sudo nmap 10.129.2.28 -Pn -n --disable-arp-ping -p 445 --reason -sV

# Trace packets (closed port — RST response)
sudo nmap 10.129.2.28 -p 21 --packet-trace -Pn -n --disable-arp-ping

# Trace packets (filtered port — no response = dropped)
sudo nmap 10.129.2.28 -p 139 --packet-trace -n --disable-arp-ping -Pn

# Trace packets (filtered port — ICMP unreachable = rejected)
sudo nmap 10.129.2.28 -p 445 --packet-trace -n --disable-arp-ping -Pn
```

## Key Options/Flags

| Flag | Meaning |
|------|---------|
| `-sS` | SYN scan — stealthy, half-open, root required |
| `-sT` | TCP Connect scan — full handshake, no root needed |
| `-sU` | UDP scan — slow, stateless |
| `-sV` | Service/version detection |
| `-p <port>` | Specific port scan |
| `-p-` | All 65535 ports scan |
| `-F` | Fast scan — top 100 ports |
| `--top-ports=X` | Top X frequent ports scan |
| `-Pn` | ICMP echo disable karo |
| `-n` | DNS resolution disable karo |
| `--reason` | Port state ka reason dikhao |

## My Lab Notes
- SYN scan (-sS) — SYN bhejta hai, SYN-ACK mile toh open, RST mile toh closed
- Connect scan (-sT) — full handshake karta hai, logs banta hai — less stealthy
- Filtered = packet dropped (no response, scan slow hoga)
- Filtered = packet rejected (ICMP type=3/code=3 milta hai, fast response)
- UDP scan bahut slow hota hai — -F flag use karo top 100 pe
- -sV version scan karta hai — service banner grab karke version identify karta hai

## References
- HTB Module: Network Enumeration with Nmap — Section 4 (Host and Port Scanning)
- Tool docs: https://nmap.org/book/man-port-scanning-techniques.html

## MITRE
T1595.001 - Active Scanning: Scanning IP Blocks
T1046 - Network Service Discovery
