# DNS Cheatsheet

## Basic Queries
| Command | Use |
|---------|-----|
| `dig ns <domain> @<DNS_IP>` | Nameservers dhundho |
| `dig soa <domain>` | SOA record |
| `dig any <domain> @<DNS_IP>` | Sabhi records |
| `dig CH TXT version.bind <DNS_IP>` | DNS server version |

## Zone Transfer
| Command | Use |
|---------|-----|
| `dig axfr <domain> @<DNS_IP>` | Full zone transfer |
| `dig axfr internal.<domain> @<DNS_IP>` | Internal zone transfer try karo |

## Subdomain Enumeration
| Command | Use |
|---------|-----|
| `for sub in $(cat wordlist);do dig $sub.<domain> @<DNS_IP> \| grep -v ';\|SOA' \| grep $sub;done` | Bash brute force |
| `dnsenum --dnsserver <IP> --enum -p 0 -s 0 -o out.txt -f wordlist <domain>` | DNSenum automated |

## Ports
| Port | Service |
|------|---------|
| 53/UDP | DNS queries |
| 53/TCP | Zone transfers, large responses |
