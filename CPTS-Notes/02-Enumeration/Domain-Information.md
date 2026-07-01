# Domain Information

## What is it?
Passive information gathering — company ki internet presence identify karna.
Direct scans nahi karte — "customer" ki tarah navigate karte hain.
SSL certs, DNS records, subdomains, third-party providers sab gather karte hain.

## When to use?
Black-box pentest ka Layer 1 (Internet Presence) — sabse pehle karo.
Active scanning se pehle passive recon karo.
Third-party hosted systems identify karo — unhe test karne ki permission nahi hoti.

## Commands

```bash
# crt.sh se subdomains nikalo (Certificate Transparency)
curl -s "https://crt.sh/?q=inlanefreight.com&output=json" | jq .

# Unique subdomains filter karo
curl -s "https://crt.sh/?q=inlanefreight.com&output=json" | jq . | grep name | cut -d":" -f2 | grep -v "CN=" | cut -d'"' -f2 | awk '{gsub(/\\n/,"\n");}1;' | sort -u

# Company hosted servers identify karo
for i in $(cat subdomainlist);do host $i | grep "has address" | grep inlanefreight.com | cut -d" " -f1,4;done

# IP list banao
for i in $(cat subdomainlist);do host $i | grep "has address" | grep inlanefreight.com | cut -d" " -f4 >> ip-addresses.txt;done

# Shodan se IP info nikalo
for i in $(cat ip-addresses.txt);do shodan host $i;done

# DNS records nikalo
dig any inlanefreight.com
```

## Key Options/Flags
| Tool/Flag | Meaning |
|-----------|---------|
| `crt.sh` | Certificate Transparency logs — subdomains milte hain |
| `dig any` | Sabhi DNS records nikalo |
| `shodan host` | IP ka open ports aur service info |
| `host <domain>` | Domain ka IP resolve karo |

## DNS Record Types
| Record | Meaning |
|--------|---------|
| A | Domain → IP address |
| MX | Mail server records |
| NS | Name server records — hosting provider identify karo |
| TXT | Verification keys, SPF, DMARC, DKIM — third-party providers |
| SOA | Start of Authority — primary DNS server info |

## TXT Records Se Kya Milta Hai
| TXT Value | Indicates |
|-----------|-----------|
| atlassian-domain-verification | Jira/Confluence use ho raha hai |
| google-site-verification | Google Workspace/Gmail |
| logmein-verification | Remote access platform |
| v=spf1 mailgun.org | Email API — IDOR/SSRF test karo |
| v=spf1 outlook | Office 365, OneDrive, Azure |
| MS= prefix | INWX hosting — domain management |

## My Lab Notes
- SSL certificate mein multiple subdomains ho sakte hain — zaroor check karo
- Third-party hosted IPs test karne ki permission nahi — pehle confirm karo scope
- TXT records = goldmine — third-party services reveal hote hain
- LogMeIn access = sab systems ka access (password reuse check karo)
- Azure file storage = SMB protocol — interesting target
- Mailgun dikh raha hai = API endpoints test karo (IDOR, SSRF)
- Google Gmail = open GDrive folders ho sakte hain

## References
- HTB Module: Footprinting — Section 3 (Domain Information)
- crt.sh: https://crt.sh
- Shodan: https://shodan.io

## MITRE
T1596.003 - Search Open Technical Databases: Digital Certificates
T1596.001 - Search Open Technical Databases: DNS/Passive DNS
T1590.001 - Gather Victim Network Information: Domain Properties
