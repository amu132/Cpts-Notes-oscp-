# Footprinting Cheatsheet

## Passive Recon - Domain Info
| Command | Use |
|---------|-----|
| `curl -s "https://crt.sh/?q=<domain>&output=json" \| jq .` | SSL cert subdomains |
| `curl -s "https://crt.sh/?q=<domain>&output=json" \| jq . \| grep name \| cut -d":" -f2 \| grep -v "CN=" \| cut -d'"' -f2 \| sort -u` | Unique subdomains filter |
| `dig any <domain>` | All DNS records |
| `host <domain>` | IP resolve karo |
| `shodan host <IP>` | IP info nikalo |
| `for i in $(cat subdomainlist);do host $i \| grep "has address" \| grep <domain> \| cut -d" " -f1,4;done` | Company hosted servers |
