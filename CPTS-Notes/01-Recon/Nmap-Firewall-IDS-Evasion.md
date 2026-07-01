# Nmap - Firewall and IDS/IPS Evasion

## What is it?
Firewall = unauthorized connections block karta hai — packets drop ya reject karta hai.
IDS = network monitor karta hai, suspicious activity pe alert deta hai.
IPS = IDS ka complement — automatically block karta hai.

Dropped packets = no response (slow scan)
Rejected packets = RST flag ya ICMP error milta hai (fast response)

## When to use?
Jab ports filtered dikh rahe ho aur firewall/IPS bypass karna ho.
Real engagement mein stealth chahiye ho.
IDS/IPS detect karna ho network mein.

## Commands

```bash
# SYN scan (firewall ke against test)
sudo nmap 10.129.2.28 -p 21,22,25 -sS -Pn -n --disable-arp-ping --packet-trace

# ACK scan (firewall rules bypass — harder to filter)
sudo nmap 10.129.2.28 -p 21,22,25 -sA -Pn -n --disable-arp-ping --packet-trace

# Decoy scan — 5 random IPs se disguise karo
sudo nmap 10.129.2.28 -p 80 -sS -Pn -n --disable-arp-ping --packet-trace -D RND:5

# OS detection — firewall rule test
sudo nmap 10.129.2.28 -n -Pn -p 445 -O

# Different source IP se scan (firewall bypass test)
sudo nmap 10.129.2.28 -n -Pn -p 445 -O -S 10.129.2.200 -e tun0

# SYN scan filtered port
sudo nmap 10.129.2.28 -p 50000 -sS -Pn -n --disable-arp-ping --packet-trace

# DNS port (53) se scan — firewall often allows port 53
sudo nmap 10.129.2.28 -p 50000 -sS -Pn -n --disable-arp-ping --packet-trace --source-port 53

# Netcat se filtered port pe connect (source port 53)
ncat -nv --source-port 53 10.129.2.28 50000
```

## Key Options/Flags
| Flag | Meaning |
|------|---------|
| `-sA` | ACK scan — firewall bypass, harder to filter |
| `-D RND:5` | 5 random decoy IPs generate karo |
| `-S <IP>` | Custom source IP use karo |
| `-e <interface>` | Specific interface se scan karo |
| `--source-port 53` | DNS port se scan — firewall often allows |
| `--dns-server <ns>` | Custom DNS server use karo |

## Key Concepts
| Concept | Detail |
|---------|--------|
| Dropped packet | No response — firewall silently block kar raha hai |
| Rejected packet | RST ya ICMP type=3 — firewall explicitly reject kar raha hai |
| ACK scan | Firewall outgoing ACK allow karta hai — unfiltered state milta hai |
| Decoy scan | Real IP hide hota hai random IPs ke beech |
| Source port 53 | Firewall DNS traffic trust karta hai — filtered ports open ho sakte hain |

## My Lab Notes
- ACK scan (`-sA`) se firewall rules map kar sakte hain — open/closed nahi batata but unfiltered batata hai
- Decoy IPs alive hone chahiye — warna SYN flood protection trigger ho sakta hai
- `--source-port 53` powerful trick hai — bahut firewalls DNS trust karte hain
- IDS detect karne ke liye — aggressive scan karo ek port pe, dekho block hote ho ya nahi
- IPS present hai toh VPS change karna padega — same IP block ho jaayegi

## References
- HTB Module: Network Enumeration with Nmap — Section 9 (Firewall and IDS/IPS Evasion)
- Nmap Docs: https://nmap.org/book/man-bypass-firewalls-ids.html

## MITRE
T1562.001 - Impair Defenses: Disable or Modify Tools
T1036 - Masquerading
T1095 - Non-Application Layer Protocol
