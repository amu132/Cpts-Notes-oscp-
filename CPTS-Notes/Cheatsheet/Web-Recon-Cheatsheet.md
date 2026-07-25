
## Fingerprinting
| Command | Use |
|---------|-----|
| curl -I <domain> | Banner grab — headers only |
| wafw00f <domain> | WAF detection |
| nikto -h <domain> -Tuning b | Fingerprinting-only scan |
| whatweb <domain> | CLI tech fingerprinting |

## Web Crawling
| Command | Use |
|---------|-----|
| pip3 install scrapy | Scrapy install |
| wget -O ReconSpider.zip <url> && unzip ReconSpider.zip | ReconSpider download |
| python3 ReconSpider.py <target_url> | Run crawler — results.json output |

## Google Dorking
| Dork | Use |
|------|-----|
| site:<domain> inurl:login | Login pages |
| site:<domain> filetype:pdf | PDF files |
| site:<domain> inurl:config.php | Config files |
| site:<domain> filetype:sql | DB backups |
| site:<domain> inurl:backup | Backup files |

## Automation Tools
| Command | Use |
|---------|-----|
| ./finalrecon.py --full --url <target> | Full recon |
| ./finalrecon.py --headers --whois --url <target> | Headers + Whois |
| ./finalrecon.py --sub --url <target> | Subdomain enum |
| ./finalrecon.py --dir --url <target> | Directory search |
| theHarvester -d <domain> -b all | Email/subdomain OSINT |
