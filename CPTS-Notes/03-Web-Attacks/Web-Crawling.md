# Web Crawling (Creepy Crawlies)

## What is it?
Web crawling = automated tools se website crawl karke hidden content, links, files discover karna.
Manual crawling ke bajaye tools use karo — fast + efficient.

## When to use?
Fingerprinting ke baad — website structure, hidden files, emails discover karne ke liye.
Permission lo pehle — intrusive scans avoid karo without consent.
Server resources ka khayal rakho — excessive requests se overload mat karo.

## Popular Web Crawlers
| Tool | Type | Use |
|------|------|-----|
| Burp Suite Spider | Active crawler | Web app mapping, hidden content, vuln discovery |
| OWASP ZAP | Free/open-source scanner | Automated + manual crawling |
| Scrapy | Python framework | Custom crawlers, structured data extraction |
| Apache Nutch | Java, scalable | Massive/large-scale crawls, more technical setup |

## Commands

# Install Scrapy
pip3 install scrapy

# Download ReconSpider (custom recon spider)
wget -O ReconSpider.zip https://academy.hackthebox.com/storage/modules/144/ReconSpider.v1.2.zip
unzip ReconSpider.zip

# Run ReconSpider against target
python3 ReconSpider.py http://inlanefreight.com

## ReconSpider Output (results.json)
| Key | Description |
|-----|-------------|
| emails | Domain pe mile email addresses |
| links | Domain ke andar mile URLs |
| external_files | External files (PDFs etc.) |
| js_files | JavaScript files used by site |
| form_fields | Forms mile (agar hain) |
| images | Image URLs |
| videos | Video URLs |
| audio | Audio file URLs |
| comments | HTML comments in source code |

## My Lab Notes
- ReconSpider ek hi command mein comprehensive JSON report deta hai — emails, links, files sab
- HTML comments (`<!-- -->`) mein sensitive info chhupi ho sakti hai — zaroor check karo
- external_files mein PDFs/docs — ye internal info leak kar sakte hain (employee names, structure)
- js_files ko manually review karo — API endpoints, hardcoded secrets mil sakte hain
- emails list se — user enumeration/phishing/OSINT ke liye directly useful
- Ethical crawling — permission lo, rate-limit rakho, server overload avoid karo

## References
- HTB Module: Information Gathering - Web Edition — Creepy Crawlies Section
- Related: "Using Web Proxies" module (CWES)

## MITRE
T1594 - Search Victim-Owned Websites
T1589.002 - Gather Victim Identity Information: Email Addresses
T1592.002 - Gather Victim Host Information: Software
