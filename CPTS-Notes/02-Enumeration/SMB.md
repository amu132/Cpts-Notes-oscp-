# SMB - Server Message Block

## What is it?
SMB = client-server protocol — files, directories, printers, network resources share karta hai.
TCP based — three-way handshake pehle hota hai.
Samba = SMB ka Linux/Unix implementation — CIFS protocol use karta hai (SMB1 dialect).

CIFS → NetBIOS ports 137, 138, 139
SMB (newer) → TCP port 445 exclusively

## When to use?
Port 139/445 open mile toh — shares, users, groups enumerate karo.
Anonymous/null session try karo — bahut info leak ho sakti hai.
Windows aur Linux dono targets pe common hai.

## SMB Versions
| Version | OS Support | Features |
|---------|-----------|----------|
| CIFS | Windows NT 4.0 | NetBIOS interface |
| SMB 1.0 | Windows 2000 | Direct TCP connection |
| SMB 2.0 | Vista, Server 2008 | Performance, message signing |
| SMB 2.1 | Windows 7, Server 2008 R2 | Locking mechanisms |
| SMB 3.0 | Windows 8, Server 2012 | Multichannel, encryption |
| SMB 3.1.1 | Windows 10, Server 2016 | Integrity check, AES-128 |

## Commands

```bash
# Nmap SMB scan
sudo nmap 10.129.14.128 -sV -sC -p139,445

# List shares (null session)
smbclient -N -L //10.129.14.128

# Connect to specific share
smbclient //10.129.14.128/notes

# RPCclient — null session connect
rpcclient -U "" 10.129.14.128

# Brute force user RIDs
for i in $(seq 500 1100);do rpcclient -N -U "" 10.129.14.128 -c "queryuser 0x$(printf '%x\n' $i)" | grep "User Name\|user_rid\|group_rid" && echo "";done

# Impacket samrdump
samrdump.py 10.129.14.128

# SMBmap
smbmap -H 10.129.14.128

# CrackMapExec — shares enum
crackmapexec smb 10.129.14.128 --shares -u '' -p ''

# Enum4linux-ng — full enumeration
./enum4linux-ng.py 10.129.14.128 -A
```

## RPCclient Queries
| Query | Description |
|-------|-------------|
| `srvinfo` | Server information |
| `enumdomains` | Sabhi domains enumerate karo |
| `querydominfo` | Domain, server, user info |
| `netshareenumall` | Sabhi shares list karo |
| `netsharegetinfo <share>` | Specific share ki info |
| `enumdomusers` | Sabhi domain users |
| `queryuser <RID>` | Specific user ki info |
| `querygroup <RID>` | Group info |

## SMBclient Commands
| Command | Use |
|---------|-----|
| `ls` | Directory listing |
| `get <file>` | File download |
| `put <file>` | File upload |
| `!<cmd>` | Local system command run karo (connection break nahi hoga) |
| `help` | Sabhi commands list |

## Dangerous Samba Config Settings
| Setting | Risk |
|---------|------|
| `browseable = yes` | Shares list ho jaate hain |
| `read only = no` | Files modify/create ho sakti hain |
| `writable = yes` | Upload allowed |
| `guest ok = yes` | Bina password access |
| `enable privileges = yes` | SID privileges honor hote hain |
| `create mask = 0777` | New files full permissions ke saath |

## Key Config Files
| File | Use |
|------|-----|
| `/etc/samba/smb.conf` | Samba main config |

## My Lab Notes
- Null session (`-N` flag) = anonymous access — pehle ye try karo
- `smbclient -N -L //<IP>` se shares list milti hai bina credentials ke
- RID brute-force se users milte hain jab `enumdomusers` restricted ho
- `enum4linux-ng.py -A` sabse comprehensive — but slow
- Nmap SMB scripts limited info dete hain — manual tools (rpcclient, smbclient) zyada deep jaate hain
- Anonymous access + writable share = file upload → webshell possible
- Password policy bhi enum4linux se milti hai — complexity, lockout threshold
- 2+ tools use karo hamesha — har tool alag info deta hai

## References
- HTB Module: Footprinting — SMB Section
- Samba man pages

## MITRE
T1021.002 - Remote Services: SMB/Windows Admin Shares
T1135 - Network Share Discovery
T1087.002 - Account Discovery: Domain Account
T1069.002 - Permission Groups Discovery: Domain Groups
