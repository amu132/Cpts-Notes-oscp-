# IMAP/POP3 Cheatsheet

## Enumeration
| Command | Use |
|---------|-----|
| `sudo nmap <IP> -sV -p110,143,993,995 -sC` | Full scan |
| `curl -k 'imaps://<IP>' --user user:pass` | IMAP login |
| `curl -k 'imaps://<IP>' --user user:pass -v` | Verbose (cert info) |
| `openssl s_client -connect <IP>:pop3s` | POP3S manual |
| `openssl s_client -connect <IP>:imaps` | IMAPS manual |

## Ports
| Port | Service |
|------|---------|
| 110 | POP3 |
| 995 | POP3S |
| 143 | IMAP |
| 993 | IMAPS |

## Quick Commands
| Protocol | Login | Retrieve | Quit |
|----------|-------|----------|------|
| IMAP | `1 LOGIN user pass` | `1 FETCH <ID> all` | `1 LOGOUT` |
| POP3 | `USER user` + `PASS pass` | `RETR id` | `QUIT` |
