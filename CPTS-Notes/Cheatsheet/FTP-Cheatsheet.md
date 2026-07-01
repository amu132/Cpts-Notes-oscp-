# FTP Cheatsheet

## Connection
| Command | Use |
|---------|-----|
| `ftp <IP>` | FTP connect karo |
| `nc -nv <IP> 21` | Netcat se banner grab |
| `telnet <IP> 21` | Telnet se connect |
| `openssl s_client -connect <IP>:21 -starttls ftp` | TLS FTP + SSL cert dekho |

## Anonymous Login
| Command | Use |
|---------|-----|
| `ftp <IP>` → username: `anonymous` | Anonymous login |
| `wget -m --no-passive ftp://anonymous:anonymous@<IP>` | Sab files download karo |

## Enumeration
| Command | Use |
|---------|-----|
| `sudo nmap -sV -p21 -sC -A <IP>` | FTP full scan |
| `sudo nmap -sV -p21 -sC -A <IP> --script-trace` | Script trace ke saath |
| `find / -type f -name ftp* 2>/dev/null \| grep scripts` | FTP NSE scripts dhundho |
| `sudo nmap --script-updatedb` | NSE database update karo |

## NSE Scripts
| Script | Use |
|--------|-----|
| `ftp-anon` | Anonymous login check |
| `ftp-syst` | Server status/version |
| `ftp-vsftpd-backdoor` | vsFTPd backdoor check |
| `ftp-brute` | Brute force |
| `ftp-bounce` | Bounce attack |

## File Operations
| Command | Use |
|---------|-----|
| `get <file>` | Single file download |
| `get "Important Notes.txt"` | Space wali file download |
| `put <file>` | File upload |
| `ls -R` | Recursive listing |
| `wget -m --no-passive ftp://anonymous:anonymous@<IP>` | All files download |

## Config Check (Post-Access)
| Command | Use |
|---------|-----|
| `cat /etc/vsftpd.conf \| grep -v "#"` | vsFTPd config dekho |
| `cat /etc/ftpusers` | Blocked users dekho |
