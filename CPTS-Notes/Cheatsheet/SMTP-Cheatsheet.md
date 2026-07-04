# SMTP Cheatsheet

## Enumeration
| Command | Use |
|---------|-----|
| `sudo nmap <IP> -sC -sV -p25` | Basic SMTP scan |
| `sudo nmap <IP> -p25 --script smtp-open-relay -v` | Open relay check |
| `telnet <IP> 25` | Manual interaction |

## Manual Commands (via telnet)
| Command | Use |
|---------|-----|
| `HELO <hostname>` | Session start |
| `EHLO <hostname>` | Extended session (shows features) |
| `VRFY <username>` | User enumeration |
| `MAIL FROM: <email>` | Sender set karo |
| `RCPT TO: <email>` | Recipient set karo |
| `DATA` | Email body start karo |
| `QUIT` | Session end |

## Ports
| Port | Use |
|------|-----|
| 25 | Default SMTP |
| 587 | STARTTLS/Authenticated |
| 465 | SMTPS (SSL/TLS) |
