

# Nmap - Host Discovery

## What is it?
Host discovery = network pe pehle pata karo kaun sa system online hai.
Most effective method: ICMP Echo Requests.
By default Nmap ARP ping karta hai ICMP se pehle (same subnet pe).
Always har scan store karo — `-oA` flag se all formats mein save hota hai.

## When to use?
Internal pentest ke start mein — pehle live hosts identify karo, phir port scan karo.
Jab poora network range diya ho client ne (e.g. 10.129.2.0/24).

## Commands

```bash
# Scan entire network range
sudo nmap 10.129.2.0/24 -sn -oA tnet | grep for | cut -d" " -f5

# Scan from IP list file
sudo nmap -sn -oA tnet -iL hosts.lst | grep for | cut -d" " -f5

# Scan multiple IPs
sudo nmap -sn -oA tnet 10.129.2.18 10.129.2.19 10.129.2.20

# Scan IP range shortcut
sudo nmap -sn -oA tnet 10.129.2.18-20

# Scan single IP
sudo nmap 10.129.2.18 -sn -oA host

# Force ICMP Echo Request with packet trace
sudo nmap 10.129.2.18 -sn -oA host -PE --packet-trace

# Check why host is alive
sudo nmap 10.129.2.18 -sn -oA host -PE --reason

# Disable ARP ping, use pure ICMP
sudo nmap 10.129.2.18 -sn -oA host -PE --packet-trace --disable-arp-ping
```

## Key Options/Flags
| Flag | Meaning |
|------|---------|
| `-sn` | Port scan disable karo |
| `-oA <name>` | All formats mein save karo (xml, nmap, gnmap) |
| `-iL <file>` | IP list file se scan karo |
| `-PE` | ICMP Echo Request use karo |
| `--packet-trace` | Sent/received packets dikhao |
| `--reason` | Host alive kyun hai dikhao |
| `--disable-arp-ping` | ARP ping band karo, sirf ICMP use karo |

## My Lab Notes
- Firewall wale hosts ICMP block kar sakte hain — inactive dikhenge even if alive
- ARP reply se bhi host alive confirm hota hai (same subnet)
- `-PE --disable-arp-ping` use karo jab pure ICMP test karna ho

## References
- HTB Module: Network Enumeration with Nmap — Section 3 (Host Discovery)
- Tool docs: https://nmap.org/book/man-host-discovery.html

## MITRE
T1595.001 - Active Scanning: Scanning IP Blocks