# Cloud Resources

## What is it?
AWS, GCP, Azure — companies ka data cloud pe hota hai.
Misconfigured cloud storage = unauthenticated access possible.
S3 buckets (AWS), Blobs (Azure), Cloud Storage (GCP) — publicly accessible ho sakte hain agar galat configure kiya ho.

## When to use?
Passive recon phase mein — Layer 1 (Internet Presence).
Domain information ke baad — cloud storage dhundho.
Source code, DNS records, Google Dorks se cloud assets identify karo.

## Commands

```bash
# Company hosted servers + cloud IPs identify karo
for i in $(cat subdomainlist);do host $i | grep "has address" | grep inlanefreight.com | cut -d" " -f1,4;done

# Google Dorks — AWS S3 buckets
# intext:"companyname" inurl:amazonaws.com

# Google Dorks — Azure Blob storage
# intext:"companyname" inurl:blob.core.windows.net
```

## Key Tools
| Tool | Use |
|------|-----|
| Google Dorks | Cloud storage URLs dhundho |
| domain.glass | Company infrastructure + Cloudflare status |
| GrayHatWarfare | AWS/Azure/GCP storage search + file filter |
| Website Source Code | Cloud URLs JS/CSS/images mein embedded hote hain |

## Google Dorks
| Dork | Use |
|------|-----|
| `intext:"company" inurl:amazonaws.com` | AWS S3 buckets |
| `intext:"company" inurl:blob.core.windows.net` | Azure Blob storage |
| `intext:"company" inurl:storage.googleapis.com` | GCP storage |

## Cloud Storage Types
| Provider | Storage Type | Risk if Misconfigured |
|----------|--------------|-----------------------|
| AWS | S3 Buckets | Public read/write access |
| Azure | Blob Storage | Unauthenticated file access |
| GCP | Cloud Storage | Public bucket access |

## What to Look For
- PDFs, text docs, presentations, code files publicly accessible
- SSH private keys (`id_rsa`) leaked in buckets — direct server access
- Source code mein hardcoded cloud URLs
- Company abbreviations bhi try karo — not just full name
- GrayHatWarfare pe file format filter karo — `.pem`, `.key`, `id_rsa` dhundho

## My Lab Notes
- Cloud provider secure hai but company ki configuration vulnerable ho sakti hai
- DNS list mein cloud storage URLs mil sakte hain — subdomain enumeration se
- Source code check karo — images/JS/CSS cloud se load ho rahe hain
- domain.glass = Cloudflare detect karna = Layer 2 (Gateway) note karo
- SSH private key mili = game over — direct login possible
- Company abbreviations bhi cloud bucket names mein use hoti hain
- GrayHatWarfare pe sort by file format karo — sensitive files jaldi milti hain

## References
- HTB Module: Footprinting — Section 4 (Cloud Resources)
- GrayHatWarfare: https://buckets.grayhatwarfare.com
- domain.glass: https://domain.glass

## MITRE
T1530 - Data from Cloud Storage
T1619 - Cloud Storage Object Discovery
T1596 - Search Open Technical Databases
