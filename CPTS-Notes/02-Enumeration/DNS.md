# DNS - Domain Name System

## What is it?
DNS = domain names ko IP addresses mein resolve karta hai.
No central database — distributed system, thousands of name servers.
Mostly unencrypted — DoT/DoH/DNSCrypt encryption solutions hain.

## When to use?
Passive + active recon dono mein — Layer 1 (Internet Presence).
Subdomains discover karne ke liye.
Zone transfer misconfig check karne ke liye — internal IPs leak ho sakte hain.

## DNS Server Types
| Type | Description |
|------|-------------|
| Root Server | TLD ke liye responsible, ICANN coordinate karta hai — 13 globally |
| Authoritative Nameserver | Specific zone ka binding answer deta hai |
| Non-authoritative Nameserver | Recursive/iterative query se info collect karta hai |
| Caching Server | Info cache karta hai specified time ke liye |
| Forwarding Server | Query forward karta hai dusre DNS server ko |
| Resolver | Local machine/router pe name resolution karta hai |

## DNS Record Types
| Record | Description |
|--------|-------------|
| A | Domain → IPv4 address |
| AAAA | Domain → IPv6 address |
| MX | Mail server records |
| NS | Domain ke nameservers |
| TXT | Verification keys, SPF, DMARC |
| CNAME | Alias for another domain |
| PTR | IP → Domain (reverse lookup) |
| SOA | Zone info + admin email |

## Commands

```bash
# NS record query — other nameservers dhundho
dig ns inlanefreight.htb @10.129.14.128

# SOA record query
dig soa www.inlanefreight.com

# DNS server version query (CHAOS class)
dig CH TXT version.bind 10.129.120.85

# ANY record query — sab available records
dig any inlanefreight.htb @10.129.14.128

# Zone transfer (AXFR) — misconfigured hone pe pura zone milta hai
dig axfr inlanefreight.htb @10.129.14.128

# Internal zone transfer — internal IPs/hostnames leak
dig axfr internal.inlanefreight.htb @10.129.14.128

# Subdomain brute force (bash loop)
for sub in $(cat /opt/useful/seclists/Discovery/DNS/subdomains-top1million-110000.txt);do dig $sub.inlanefreight.htb @10.129.14.128 | grep -v ';\|SOA' | sed -r '/^\s*$/d' | grep $sub | tee -a subdomains.txt;done

# DNSenum — automated enumeration
dnsenum --dnsserver 10.129.14.128 --enum -p 0 -s 0 -o subdomains.txt -f /opt/useful/seclists/Discovery/DNS/subdomains-top1million-110000.txt inlanefreight.htb
```

## Dangerous Settings (Bind9)
| Option | Risk |
|--------|------|
| `allow-query` | Kaun query bhej sakta hai control karta hai |
| `allow-recursion` | Kaun recursive query bhej sakta hai |
| `allow-transfer` | Kaun zone transfer le sakta hai — `any` set hui toh sabko access mil jaata hai! |
| `zone-statistics` | Zone stats collect karta hai |

## Key Config Files
| File | Use |
|------|-----|
| `/etc/bind/named.conf.local` | Zone definitions |
| `/etc/bind/named.conf.options` | Global options |
| `/etc/bind/db.domain.com` | Zone file — forward records |
| `/etc/bind/db.10.129.14` | Reverse zone file — PTR records |

## Zone Transfer Concepts
- **Primary/Master** = original zone data yahan hoti hai
- **Secondary/Slave** = master se zone data leta hai
- **AXFR** = full zone transfer — TCP port 53
- `allow-transfer = any` misconfigured hai toh koi bhi pura zone file access kar sakta hai — internal hostnames + IPs leak

## My Lab Notes
- `dig any` se saare records ek saath milte hain — lekin sab zones show nahi hoti
- Zone transfer (`axfr`) test zaroor karo har discovered nameserver pe
- Internal subdomain zone transfer alag test karo (e.g. `internal.domain.htb`) — jackpot mil sakta hai
- `version.bind` query se DNS server version milta hai (agar record exist karta ho)
- Subdomain brute-force ke liye SecLists use karo — dnsenum automate kar deta hai
- TXT records mein SPF/DMARC se third-party services identify hoti hain (same as domain info section)

## References
- HTB Module: Footprinting — DNS Section
- SecLists: /opt/useful/seclists/Discovery/DNS/

## MITRE
T1590.002 - Gather Victim Network Information: DNS
T1596.001 - Search Open Technical Databases: DNS/Passive DNS
T1018 - Remote System Discovery
