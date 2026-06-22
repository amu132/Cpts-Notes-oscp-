
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
|Command|Use|
|---|---|
|`nmap <target> -oA scan`|Save in all formats (.nmap, .xml, .gnmap)|
|`nmap <target> -oN scan.nmap`|Save normal output|
|`nmap <target> -oG scan.gnmap`|Save grepable output|
|`nmap <target> -oX scan.xml`|Save XML output|
|`xsltproc scan.xml -o scan.html`|Convert XML report to HTML|


# Service Version Detection
| Command                                  | Use                                    |
| ---------------------------------------- | -------------------------------------- |
| `nmap -sV <target>`                      | Service version detection              |
| `nmap -p- -sV <target>`                  | Scan all ports + detect versions       |
| `nmap -p- -sV -v <target>`               | Verbose service detection              |
| `nmap -p- -sV -vv <target>`              | Extra verbose output                   |
| `nmap -p- -sV --stats-every=5s <target>` | Show scan progress every 5 seconds     |
| `nmap -sV --packet-trace <target>`       | Show sent/received packets             |
| `nmap -sV -Pn -n <target>`               | Skip host discovery and DNS resolution |
|                                          |                                        |
|                                          |                                        |

Banner grabbing

|Command|Use|
|---|---|
|`nc -nv <target> <port>`|Grab service banner manually|
|`nc -nv <target> 25`|Grab SMTP banner|
|`nc -nv <target> 21`|Grab FTP banner|
|`nc -nv <target> 110`|Grab POP3 banner|
|`telnet <target> <port>`|Alternative banner grabbing|

Common Enumeration Workflow

|Command|Use|
|---|---|
|`nmap -p- --min-rate 1000 <target>`|Initial full port discovery|
|`nmap -sC -sV -p <ports> <target>`|Enumerate discovered services|
|`nc -nv <target> <port>`|Manual banner grabbing|
|`searchsploit <service>`|Search for exploits|
|`curl http://<target>`|Quick HTTP enumeration|


## Performance
| Command | Use |
|---------|-----|
| `nmap -T0` | Paranoid — IDS evasion |
| `nmap -T3` | Normal — default |
| `nmap -T5` | Insane — fastest |
| `nmap --min-rate 300` | 300 packets/sec |
| `nmap --max-retries 0` | No retries — fast |
| `nmap --max-rtt-timeout 100ms` | RTT limit |
