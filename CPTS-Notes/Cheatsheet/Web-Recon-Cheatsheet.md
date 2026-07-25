
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
