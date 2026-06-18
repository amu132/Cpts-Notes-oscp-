
# Nmap Cheatsheet

## Host Discovery
| Command                                | Use                      |
| -------------------------------------- | ------------------------ |
| `nmap -sn 10.10.10.0/24`               | Network range scan       |
| `nmap -sn -iL hosts.lst`               | IP list se scan          |
| `nmap -sn -PE --disable-arp-ping <IP>` | Pure ICMP scan           |
| `nmap -sn --reason <IP>`               | Host alive reason dikhao |
| `nmap -sn --packet-trace <IP>`         | Packets dikhao           |

## Output Formats
| Flag | Format |
|------|--------|
| `-oA <name>` | All formats (xml, nmap, gnmap) |
| `-oN <name>` | Normal |
| `-oX <name>` | XML |
| `-oG <name>` | Grepable |


## Port Scanning
| Command | Use |
|---------|-----|
| `nmap -sS <IP>` | SYN scan (stealthy) |
| `nmap -sT <IP>` | TCP Connect scan |
| `nmap -sU -F <IP>` | UDP fast scan |
| `nmap -sV <IP>` | Version detection |
| `nmap -p- <IP>` | All ports |
| `nmap -F <IP>` | Top 100 ports |
| `nmap --top-ports=10 <IP>` | Top 10 ports |

## Port States
| State | Reason |
|-------|--------|
| open | SYN-ACK mila |
| closed | RST mila |
| filtered | No response (dropped) ya ICMP type=3 (rejected) |
| open\|filtered | UDP — no response |


# Save all output formats
nmap <target> -oA scan

# Save normal output
nmap <target> -oN scan.nmap

# Save grepable output
nmap <target> -oG scan.gnmap

# Save XML output
nmap <target> -oX scan.xml

# Convert XML to HTML
xsltproc scan.xml -o scan.html