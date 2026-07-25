# Automating Recon

## What is it?
Manual recon time-consuming + error-prone hota hai.
Automation tools = efficiency, scalability, consistency, comprehensive coverage.

## Why Automate?
| Benefit | Description |
|---------|-------------|
| Efficiency | Tools fast repetitive tasks karte hain |
| Scalability | Multiple targets/domains ek saath scan ho sakte hain |
| Consistency | Predefined rules — reproducible results |
| Comprehensive Coverage | DNS, subdomains, crawling, port scan sab ek saath |
| Integration | Other tools/platforms ke saath easily integrate |

## When to use?
Manual recon ke baad ya parallel mein — comprehensive coverage ke liye.
Large scope (multiple domains) ho toh especially useful.

## Reconnaissance Frameworks
| Tool | Focus |
|------|-------|
| FinalRecon | Python — SSL, whois, headers, crawling, all-in-one |
| Recon-ng | Modular framework — DNS, subdomain, port scan, exploits |
| theHarvester | Emails, subdomains, hosts, employee names, banners |
| SpiderFoot | OSINT automation — IPs, domains, emails, social media |
| OSINT Framework | Tools/resources collection — wide OSINT coverage |

## FinalRecon — Detailed

### Features
- Header Information — server details, tech, misconfigs
- Whois Lookup — domain registration info
- SSL Certificate Info — validity, issuer
- Crawler — HTML/CSS/JS, internal/external links, robots.txt, sitemap.xml
- DNS Enumeration — 40+ record types including DMARC
- Subdomain Enumeration — crt.sh, AnubisDB, ThreatMiner, CertSpotter, Shodan API etc.
- Directory Enumeration — custom wordlists support
- Wayback Machine — last 5 years URLs

## Commands

```bash
# Install FinalRecon
git clone https://github.com/thewhiteh4t/FinalRecon.git
cd FinalRecon
pip3 install -r requirements.txt
chmod +x ./finalrecon.py

# Help menu
./finalrecon.py --help

# Headers + Whois combined scan
./finalrecon.py --headers --whois --url http://inlanefreight.com
```

## FinalRecon Options
| Flag | Description |
|------|-------------|
| --url | Target URL specify karo |
| --headers | Header info |
| --sslinfo | SSL cert info |
| --whois | Whois lookup |
| --crawl | Website crawl |
| --dns | DNS enumeration |
| --sub | Subdomain enumeration |
| --dir | Directory search |
| --wayback | Wayback URLs |
| --ps | Fast port scan |
| --full | Full recon (sab modules ek saath) |

## Extra Options
| Flag | Use |
|------|-----|
| -dt | Directory enum threads (default 30) |
| -pt | Port scan threads (default 50) |
| -w | Custom wordlist path |
| -e | File extensions filter |
| -o | Export format |
| -k | API key add karo (e.g. shodan@key) |

## My Lab Notes
- `--full` flag = ek command mein sab kuch — headers, whois, DNS, subdomains, crawl, ports
- API keys add karna (`-k`) subdomain enumeration ko aur powerful banata hai (Shodan, VirusTotal etc.)
- Results automatically export hote hain — `~/.local/share/finalrecon/dumps/` mein
- theHarvester specifically emails/employee OSINT ke liye best
- Automation manual recon ka replacement nahi — supplement hai, dono combine karo

## References
- HTB Module: Information Gathering - Web Edition — Automating Recon
- FinalRecon: https://github.com/thewhiteh4t/FinalRecon

## MITRE
T1595 - Active Scanning
T1590 - Gather Victim Network Information
T1591 - Gather Victim Org Information
T1596 - Search Open Technical Databases
