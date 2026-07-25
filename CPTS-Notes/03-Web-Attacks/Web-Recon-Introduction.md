# Web Reconnaissance - Introduction

## Active Reconnaissance
Target se directly interact karte ho — detection risk zyada.

| Technique | Description | Tools | Detection Risk |
|-----------|-------------|-------|-----------------|
| Port Scanning | Open ports/services identify | Nmap, Masscan | High |
| Vulnerability Scanning | Known vulns probe karo | Nessus, OpenVAS, Nikto | High |
| Network Mapping | Topology map karo | Traceroute, Nmap | Medium-High |
| Banner Grabbing | Service banners retrieve | Netcat, curl | Low |
| OS Fingerprinting | OS identify karo | Nmap -O, Xprobe2 | Low |
| Service Enumeration | Service versions | Nmap -sV | Low |
| Web Spidering | Pages/directories crawl | Burp Suite Spider, OWASP ZAP | Low-Medium |

## Passive Reconnaissance
Target se direct interact nahi karte — stealthy, but info kam mil sakti hai.

| Technique | Description | Tools | Detection Risk |
|-----------|-------------|-------|-----------------|
| Search Engine Queries | Google dorking, social profiles | Google, Shodan | Very Low |
| WHOIS Lookups | Domain registration details | whois | Very Low |
| DNS Analysis | Subdomains, mail servers | dig, dnsenum, fierce, dnsrecon | Very Low |
| Web Archive Analysis | Historical website snapshots | Wayback Machine | Very Low |
| Social Media Analysis | Employee info, roles | LinkedIn, Twitter | Very Low |
| Code Repositories | Exposed creds/code | GitHub, GitLab | Very Low |

## My Lab Notes
- Active recon = more comprehensive but detection risk high — IDS/IPS trigger ho sakta hai
- Passive recon = stealthy, safe starting point — hamesha pehle karo
- Web spidering (Burp/ZAP) se hidden directories/files milte hain
- Banner grabbing low-risk hai but logged ho sakta hai — careful raho
- Combination approach best hai — passive se pehle overview lo, phir active se deep dive

## References
- HTB Module: Information Gathering - Web Edition — Introduction

## MITRE
T1595 - Active Scanning
T1592 - Gather Victim Host Information
T1589 - Gather Victim Identity Information
T1590 - Gather Victim Network Information
T1591 - Gather Victim Org Information
T1593 - Search Open Websites/Domains
