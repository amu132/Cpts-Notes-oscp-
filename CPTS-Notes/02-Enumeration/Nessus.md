# Nessus - Vulnerability Scanner

## What is it?
Nessus = industry-standard vulnerability scanner, Tenable ka product.
Scan templates 3 categories mein: Discovery, Vulnerabilities, Compliance.
Plugins (NASL language) se CVEs detect karta hai.

## When to use?
Vulnerability assessment phase mein.
Client budget/scope limited ho (full pentest nahi) tab bhi useful — cursory assessment.
Credentialed scan ho toh deep visibility milti hai.

## Scan Types
| Type | Use |
|------|-----|
| Host Discovery | Live hosts/open ports identify |
| Basic Network Scan | Standard vuln scan |
| Advanced Scan | Full customization |
| Malware Scan | Malware detection |
| Web Application Tests | Web app specific |
| Credentialed Patch Audit | Patch level check with creds |

## Scan Configuration Sections

### Discovery
- Fragile devices (printers) — disabled by default, warna garbage print ho sakta hai
- Port scanning — common/all/custom range
- Service discovery — probe all ports (default on), SSL/TLS cert check

### Assessment
- Web application scanning — custom user-agent, RFI testing URL
- Credentialed auth OR brute-force (username/password lists)
- User enumeration — SAM Registry, ADSI Query, WMI Query, RID Brute Forcing (Start/End UID)

### Advanced
- Safe checks — enabled by default (harmful checks avoid karta hai)
- Network congestion throttling
- Unresponsive host handling
- Random IP scan order option

## Scan Policies
Custom scans save karke reuse kar sakte ho — evasive scan, web-focused scan, client-specific creds.
New Policy → base scan type choose karo → customize → save → "User Defined" tab mein milega future scans ke liye.

## Nessus Plugins
- NASL (Nessus Attack Scripting Language) mein likhe hote hain
- Severity levels: Critical, High, Medium, Low, Info
- 145,973+ plugins, 58,391+ CVE IDs cover karte hain (at time of writing)
- Plugin Rules — false positives exclude/hide kar sakte ho (host + Plugin ID specify karke)

## Credentialed Scanning
| Auth Type | Supported Methods |
|-----------|---------------------|
| Linux/SSH | Password, public key, certificate, Kerberos |
| Windows | Password, Kerberos, LM hash, NTLM hash |
| Databases | Oracle, PostgreSQL, DB2, MySQL, SQL Server, MongoDB, Sybase |
| Plaintext services | FTP, HTTP, IMAP, IPMI, Telnet |

Sample creds format (lab): `htb-student_adm:HTB_@cademy_student!` (Linux), `administrator:Academy_VA_adm1!` (Windows)

## Working with Scan Output

### Report Formats
| Format | Use |
|--------|-----|
| PDF/HTML | Executive Summary or custom — sharing ke liye |
| CSV | Column selection — Splunk jaisa tool mein import ke liye |
| .nessus | XML — scan settings + plugin outputs |
| .db | .nessus + KB + Audit Trail + attachments |

⚠️ Nessus reports final deliverable NAHI hain — sirf appendix/supplementary data client report ke saath.

## Commands

```bash
# sslscan — manual verify for false positives (e.g. weak cipher suites)
sslscan example.com

# nessus-report-downloader — CLI se reports download
./nessus_downloader.rb
```

## My Lab Notes
- Web console access: `https://<IP>:8834`
- Credentialed scan = far more accurate + deep results (patch level, local vulns)
- Plugin Rules use karo known false positives (e.g. self-signed certs, by-design configs) hide karne ke liye
- CSV export = automation/analytics ke liye best (Splunk integration)
- Full pentest report mein Nessus raw output kabhi mat do — apna analysis + context zaroori hai
- RID Brute Forcing = domain/local users enumerate karne ka Nessus feature
- Safe checks always ON rakho production environments mein — harmful checks avoid

## References
- HTB Module: Vulnerability Assessment — Nessus Sections
- Tenable Plugin Database: https://www.tenable.com/plugins

## MITRE
T1595.002 - Active Scanning: Vulnerability Scanning
T1592 - Gather Victim Host Information
