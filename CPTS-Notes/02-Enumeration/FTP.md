# FTP - File Transfer Protocol

## What is it?
FTP = File Transfer Protocol — TCP port 21 (control) + TCP port 20 (data).
TFTP = Trivial FTP — UDP pe, no authentication, sirf local networks mein.
vsFTPd = most common FTP server on Linux.

Active FTP = server client se connect karta hai (firewall block kar sakta hai)
Passive FTP = client server se connect karta hai (firewall friendly)

## When to use?
Service enumeration mein — port 21 open mile toh.
Anonymous login check karo — sensitive files mil sakti hain.
Upload possible hai toh — webshell upload karke RCE possible.

## FTP Commands (Client Side)
| Command | Use |
|---------|-----|
| `ls` | Directory listing |
| `ls -R` | Recursive listing (agar ls_recurse_enable=YES) |
| `get <file>` | File download karo |
| `put <file>` | File upload karo |
| `status` | Connection status dekho |
| `debug` | Debug mode on karo |
| `trace` | Packet trace on karo |
| `exit` | FTP session band karo |

## TFTP Commands
| Command | Use |
|---------|-----|
| `connect <host>` | Remote host set karo |
| `get <file>` | File download karo |
| `put <file>` | File upload karo |
| `status` | Current status dekho |
| `quit` | Exit karo |

## Dangerous vsFTPd Settings
| Setting | Risk |
|---------|------|
| `anonymous_enable=YES` | Anonymous login allowed |
| `anon_upload_enable=YES` | Anonymous upload allowed |
| `anon_mkdir_write_enable=YES` | Anonymous folder create kar sakta hai |
| `no_anon_password=YES` | Password nahi maangega |
| `write_enable=YES` | STOR/DELE commands allowed |
| `hide_ids=YES` | UID/GID hide hota hai — ownership pata nahi chalta |
| `ls_recurse_enable=YES` | Recursive listing allowed |

## Key Config Files
| File | Use |
|------|-----|
| `/etc/vsftpd.conf` | vsFTPd main config |
| `/etc/ftpusers` | Blocked users list |

## Attack Surface
- Anonymous login → sensitive files
- Upload allowed → webshell → RCE
- FTP logs → LFI → RCE
- TLS/SSL certificate → hostname + email leak
- hide_ids=NO → real usernames visible → brute-force possible

## My Lab Notes
- Banner (220) mein version info hota hai — note karo
- Anonymous login = `ftp 10.x.x.x` → username: `anonymous`
- `ls -R` se poora structure ek baar mein dikh jaata hai
- wget se sab files ek saath download ho jaati hain — noisy hota hai
- Upload possible + web server = webshell upload karo → RCE
- TLS FTP pe openssl use karo — SSL cert mein hostname/email milta hai
- TFTP mein directory listing nahi hoti

## References
- HTB Module: Footprinting — FTP Section
- vsFTPd docs: http://vsftpd.beasts.org/

## MITRE
T1021.002 - Remote Services: SMB/FTP
T1078 - Valid Accounts (Anonymous)
T1105 - Ingress Tool Transfer
T1190 - Exploit Public-Facing Application
