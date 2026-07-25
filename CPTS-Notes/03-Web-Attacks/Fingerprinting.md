# Web Fingerprinting
## What is it?
Fingerprinting = target ki technical details extract karna (web server, OS, software components).
Digital signature jaisa — infrastructure aur weaknesses reveal karta hai.
## Why Important?
| Reason | Benefit |
|--------|---------|
| Targeted Attacks | Specific exploits/vulns focus kar sakte ho |
| Identifying Misconfigurations | Outdated software, default settings expose hote hain |
| Prioritising Targets | Multiple targets mein sabse weak identify karo |
| Comprehensive Profile | Sabhi recon findings combine karke pura picture banta hai |
## When to use?
Passive recon ke baad — pehle technology stack samjho.
WAF check karo pehle — further probes block ho sakte hain.
## Fingerprinting Techniques
| Technique | Description |
|-----------|-------------|
| Banner Grabbing | Server banners analyze karo — software/version reveal hota hai |
| HTTP Headers Analysis | Server, X-Powered-By headers — tech stack info |
| Probing Specific Responses | Crafted requests se unique responses elicit karo |
| Page Content Analysis | Structure, scripts, copyright info se clues milte hain |
## Tools
| Tool | Purpose |
|------|---------|
| Wappalyzer | Browser extension — tech profiling |
| BuiltWith | Detailed tech stack reports |
| WhatWeb | CLI fingerprinting — signature database |
| Nmap | Service/OS fingerprinting (NSE scripts) |
| Netcraft | Hosting + security posture reports |
| wafw00f | WAF detection specifically |
| Nikto | Vulnerability + fingerprinting scanner |
## Commands
# Banner grabbing — HTTP headers only
curl -I inlanefreight.com
# Follow redirects — grab banners at each hop
curl -I https://inlanefreight.com
curl -I https://www.inlanefreight.com
# WAF detection
pip3 install git+https://github.com/EnableSecurity/wafw00f
wafw00f inlanefreight.com
# Nikto — fingerprinting only (Software Identification modules)
nikto -h inlanefreight.com -Tuning b
# Nikto setup (if not pre-installed)
sudo apt update && sudo apt install -y perl
git clone https://github.com/sullo/nikto
cd nikto/program
chmod +x ./nikto.pl
## Key Headers to Check
| Header | Reveals |
|--------|---------|
| Server | Web server software + version |
| X-Powered-By | Scripting language/framework |
| X-Redirect-By | CMS (e.g. WordPress) |
| Link (wp-json) | WordPress REST API — confirms WP |
## My Lab Notes
- `curl -I` sirf headers fetch karta hai — fast aur lightweight
- Redirect chains follow karo — har hop pe naya banner mil sakta hai
- `X-Redirect-By: WordPress` jaisa header directly CMS confirm kar deta hai
- WAF check ALWAYS pehle karo — Wordfence jaisa WAF requests block/filter kar sakta hai
- `wafw00f` minimal requests bhejta hai (~2 requests) — stealthy hai
- Nikto `-Tuning b` flag = sirf software identification, poora vuln scan nahi (faster + focused)
- Nikto se license.txt, outdated Apache version, missing security headers (HSTS, X-Content-Type-Options) sab milta hai
- `/wp-login.php` mil jaaye toh WordPress-specific attacks (brute-force, plugin vulns) explore karo
## References
- HTB Module: Information Gathering - Web Edition — Fingerprinting Section
## MITRE
T1592.002 - Gather Victim Host Information: Software
T1590.006 - Gather Victim Network Information: Network Security Appliances (WAF)
T1595.002 - Active Scanning: Vulnerability Scanning
