# IMAP / POP3

## What is it?
IMAP = online email management, server pe hi folders/emails manage hote hain, sync across devices.
POP3 = simple — list, retrieve, delete only. No server-side folder management.
Dono unencrypted by default — SSL/TLS use karo.

Ports:
- IMAP: 143 (plain), 993 (SSL/TLS)
- POP3: 110 (plain), 995 (SSL/TLS)

## When to use?
Port 110/143/993/995 open mile toh.
Credentials mil jaayein (SMTP VRFY se ya kahin aur se) toh login try karo — emails read kar sakte ho.

## Commands

```bash
# Nmap scan - all 4 ports
sudo nmap 10.129.14.128 -sV -p110,143,993,995 -sC

# cURL se IMAP login (SSL)
curl -k 'imaps://10.129.14.128' --user user:password

# cURL verbose - cert + banner info
curl -k 'imaps://10.129.14.128' --user cry0l1t3:1234 -v

# OpenSSL - POP3S manual interaction
openssl s_client -connect 10.129.14.128:pop3s

# OpenSSL - IMAPS manual interaction
openssl s_client -connect 10.129.14.128:imaps
```

## IMAP Commands
| Command | Description |
|---------|-------------|
| `1 LOGIN username password` | Login karo |
| `1 LIST "" *` | Sabhi directories list karo |
| `1 CREATE "INBOX"` | Mailbox banao |
| `1 DELETE "INBOX"` | Mailbox delete karo |
| `1 SELECT INBOX` | Mailbox select karo |
| `1 FETCH <ID> all` | Message data retrieve karo |
| `1 LOGOUT` | Connection close karo |

## POP3 Commands
| Command | Description |
|---------|-------------|
| `USER username` | User identify karo |
| `PASS password` | Password authenticate karo |
| `STAT` | Saved emails count |
| `LIST` | Emails ki size/number |
| `RETR id` | Specific email retrieve karo |
| `DELE id` | Email delete karo |
| `CAPA` | Server capabilities dikhao |
| `QUIT` | Connection close karo |

## Dangerous Settings (Dovecot)
| Setting | Risk |
|---------|------|
| `auth_debug` | Debug logging enabled |
| `auth_debug_passwords` | Passwords log mein aa sakte hain |
| `auth_verbose_passwords` | Auth passwords logged (truncated) |
| `auth_anonymous_username` | Anonymous login username defined |

## My Lab Notes
- SSL cert se organization, hostname, location info milti hai (same as FTP/SMTP)
- `curl -v` use karo — TLS version, cert details, banner sab milta hai
- Credentials mil jaaye (weak passwords like username=password) toh directly login try karo
- Nmap scan se capabilities milti hain — supported commands identify karo
- POP3/IMAP dono higher ports (993/995) SSL use karte hain by default

## References
- HTB Module: Footprinting — IMAP/POP3 Section
- Dovecot docs

## MITRE
T1114.002 - Email Collection: Remote Email Collection
T1078 - Valid Accounts
EOF
