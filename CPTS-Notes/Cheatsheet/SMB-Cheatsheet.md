# SMB Cheatsheet

## Enumeration
| Command | Use |
|---------|-----|
| `sudo nmap <IP> -sV -sC -p139,445` | Nmap SMB scan |
| `smbclient -N -L //<IP>` | Null session — share listing |
| `smbclient //<IP>/<share>` | Share se connect |
| `rpcclient -U "" <IP>` | Null session RPC connect |
| `smbmap -H <IP>` | Shares + permissions |
| `crackmapexec smb <IP> --shares -u '' -p ''` | Shares enum |
| `./enum4linux-ng.py <IP> -A` | Full automated enum |
| `samrdump.py <IP>` | Impacket user enum |

## RPCclient Queries
| Query | Use |
|-------|-----|
| `srvinfo` | Server info |
| `enumdomusers` | All users |
| `netshareenumall` | All shares |
| `queryuser <RID>` | User details |
| `querygroup <RID>` | Group details |

## RID Brute Force
```bash
for i in $(seq 500 1100);do rpcclient -N -U "" <IP> -c "queryuser 0x$(printf '%x\n' $i)" | grep "User Name\|user_rid\|group_rid" && echo "";done
```

## SMBclient Session Commands
| Command | Use |
|---------|-----|
| `ls` | List files |
| `get <file>` | Download |
| `put <file>` | Upload |
| `!<cmd>` | Local command |

## Ports
| Port | Service |
|------|---------|
| 139 | NetBIOS SMB |
| 445 | SMB direct (modern) |
